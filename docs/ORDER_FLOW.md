
## Order Saga – Synchronous Orchestration (Current Implementation)

The Order Service implements a Saga Orchestrator to manage distributed order workflows.

### Why synchronous saga?
- Easier reasoning for core business flow
- Clear compensation handling
- Deterministic state transitions

### Known trade-offs
- Tighter coupling
- Higher latency
- Limited scalability

### Future evolution
- Event-driven saga using Kafka
- Step-based state machine
- Timeout & retry handling


### Code Implementation

    public class OrderSagaOrchestrator {
    
      private final InventoryClient inventoryClient;
      private final PaymentClient paymentClient;
      private final OrderRepository orderRepository;
  
      @Transactional
      public Order processOrderSaga(Order order) {
  
          if (!inventoryClient.reserveInventory(order.getId(), order.getItems())) {
              return cancelOrder(order);
          }
  
          updateStatus(order, OrderStatus.INVENTORY_RESERVED);
  
          boolean paymentSuccess = paymentClient.processPayment(order.getId(), order.getPayableAmount());
  
          if (!paymentSuccess) {
              Boolean isReleased = inventoryClient.releaseInventory(order.getId());
              if(Objects.isNull(isReleased) || !isReleased) {
                  log.info("Order {} has not been released.", order.getId());
              }
              return updateStatus(order, OrderStatus.PAYMENT_FAILED);
          }
          Boolean isCommited = inventoryClient.commitInventory(order.getId());
  
          if (Objects.nonNull(isCommited) && isCommited) {
              log.info("Order {} has been committed.", order.getId());
              return updateStatus(order, OrderStatus.CONFIRMED);
          }
          log.info("Order {} has not been committed", order.getId());
          return cancelOrder(order);
      }
  
      private Order cancelOrder(Order order) {
          return updateStatus(order, OrderStatus.CANCELLED);
      }
  
      private Order updateStatus(Order order, OrderStatus status) {
          order.setStatus(status);
          order.setUpdatedAt(Instant.now());
          return orderRepository.save(order);
      }
    }
