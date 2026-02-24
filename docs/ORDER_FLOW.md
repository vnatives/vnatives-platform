
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
