
# Database Relations Roadmap: Laravel Modular Monolith → Microservices

---

## Phase 1: Modular Monolith (Single App, Multiple Modules)

### Database Strategy
- **Single Database**
- Clear **schema boundaries per module** (tables prefixed or schema-based)
- No shared Eloquent Models across modules

### Relationship Handling
- Eloquent relationships allowed **only inside the same module**
- Cross-module relations must be:
  - Replaced with **foreign keys as raw IDs**
  - Accessed via **Service Layer / Repository**
  - Never via `belongsTo`, `hasMany` across modules

### Rules
- ❌ No cross-module joins
- ❌ No cross-module Eloquent relationships
- ✅ Module-to-module communication via:
  - Interfaces
  - Domain Services
  - Events (internal)

### Goal of This Phase
- Enforce **logical isolation**
- Prepare codebase for DB separation without refactoring logic

---

## Phase 2: Modular Monolith with Database-per-Module

### Database Strategy
- **Multiple databases**
  - One database per module
- Separate DB connections per module
- Central app still deployed as **one Laravel project**

### Relationship Handling
- ❌ No foreign keys across databases
- Replace relations with:
  - `*_id` references only
  - Explicit fetch through module services
- Introduce **DTOs** between modules

### Communication Patterns
- Internal synchronous calls:
  - `UserService::getById($id)`
- Internal async events:
  - Domain Events
  - Queue-based listeners

### Data Consistency
- Eventual consistency
- Compensating actions instead of transactions
- No distributed transactions

### Goal of This Phase
- Break **database coupling**
- Simulate microservice constraints inside one codebase

---

## Phase 3: Laravel Microservices (Independent Services)

### Database Strategy
- **Database per Service**
- Zero shared databases
- Zero shared schemas
- Zero shared migrations

### Relationship Handling
- ❌ No relational joins across services
- ❌ No foreign keys across services
- Relationships become:
  - API calls
  - Events
  - Cached projections

### Communication Patterns
- Sync:
  - REST / gRPC APIs
- Async:
  - Message broker (Kafka / RabbitMQ / Redis Streams)
- Data contracts required

### Data Patterns
- API Composition
- Event-driven projections
- CQRS (optional)
- Saga Pattern for workflows

### Example
- Attendance Service stores `student_id`
- Student Service owns student data
- Attendance queries student data via API or local read-model

### Goal of This Phase
- Full service autonomy
- Independent scaling and deployment
- Technology flexibility

---

## Phase 4 (Optional): Advanced Distributed Data Patterns

### Enhancements
- Read Replicas per service
- Materialized views via events
- API Gateway aggregation
- Global Search Index (Elastic / OpenSearch)

### Advanced Consistency
- Saga orchestration
- Choreographed events
- Idempotent consumers

### Goal of This Phase
- High scalability
- Fault isolation
- Enterprise-grade resilience

---

## Key Transition Principles (Non‑Negotiable)

- Relationships move from **Eloquent → Services → APIs**
- IDs are references, not relations
- Ownership of data is absolute
- One service = one source of truth
- No rollback across services

---

## Final Mental Model

| Stage | Relationship Style |
|------|-------------------|
| Modular Monolith | Eloquent (internal only) |
| Multi‑DB Modular | Service‑based |
| Microservices | API / Events |
| Distributed | Eventual Consistency |

---

**If it joins, it does not scale.**  
**If it queries remotely, it survives.**
