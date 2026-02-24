
## Order Saga – Synchronous Orchestration (Current Implementation)

The Order Service implements a Saga Orchestrator to manage distributed order workflows involving Inventory and Payment services.

This implementation is explicitly designed to handle failures, compensation, and partial success scenarios in a distributed system.

### 🎯 Why a Synchronous Saga?

This implementation intentionally uses synchronous orchestration instead of events.

Reasons:
- Easier reasoning about core business invariants
- Explicit control over compensation steps
- Deterministic order state transitions
- Simpler debugging during early system evolution

The focus here is correctness and clarity over maximum scalability.

### 🔁 Saga Flow Summary

- Order is created
- Inventory is reserved
- Payment is processed
- Inventory is committed
- Order is confirmed
  
If any step fails, compensation logic is triggered and the order is moved to a safe terminal state.

### 🔥 Failure Handling (Non-Happy Path)

This saga explicitly handles real-world failure scenarios:

- ❌ Inventory reservation failure → Order is cancelled
- ❌ Payment failure → Inventory is released, order marked as PAYMENT_FAILED
- ❌ Inventory commit failure → Order is cancelled
- ❌ Partial execution → State transitions are persisted and retried safely

No step assumes success by default.

### ⚠️ Known Trade-offs

This design makes the following explicit trade-offs:

- Tighter coupling via synchronous REST calls
- Higher end-to-end latency
- Limited horizontal scalability for high traffic
 
These trade-offs are intentional and acknowledged, not accidental.

### 🔮 Future Evolution (Planned)

The saga is designed to evolve without changing business logic:

- Event-driven saga using Kafka
- Step-based state machine persisted in DB
- Timeout & retry handling per step
- Idempotent event consumers
- Asynchronous compensation workflows

The core state machine remains the same — only the transport changes.


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

### Notes:
- 📊 Refer to `docs/flowDiagram/orderFlow/PlantUML.png` for the failure-aware saga flow diagram.
