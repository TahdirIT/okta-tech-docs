# Microservices Readiness Prerequisites

Before transitioning to a microservices architecture, the system must meet the following conditions:

- Each service must have **clear data ownership** and manage its own database independently.
- There must be **no cross-database joins**, shared tables, or foreign keys between services.
- All inter-service relationships must be expressed through **explicit contracts** (APIs or events), not database-level coupling.
- Services must be **deployable, scalable, and operable independently**.
- Data consistency must be handled through **event-driven workflows** or **saga-based coordination**, not distributed transactions.
- Service interfaces must be **versioned and backward-compatible**.
- The system must support **centralized logging, distributed tracing, and correlation IDs** for effective debugging.
- Read operations that require data from multiple services must rely on **aggregation layers or read models**, not synchronous service chaining.
- Configuration and secrets must be **resolved at runtime**, avoiding hard-coded values or environment-bound dependencies inside services.

---

**Status:** Microservices-Ready Checklist

