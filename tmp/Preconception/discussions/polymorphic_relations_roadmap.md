# Polymorphic Relations Across Services – Roadmap

---

## Phase 1: Modular Monolith (Laravel Modules)

**Goal:** Isolate polymorphic relations to module boundaries without breaking database integrity.

### Key Principles
- Polymorphic relations are **allowed only inside the same module**.
- No cross-module `morphTo`, `morphMany`, or `morphOne`.
- Shared concepts are treated as **Reference IDs**, not Eloquent relations.

### Recommended Patterns

#### 1. Replace Cross‑Module Polymorphism with Explicit Columns
Instead of:
```php
morphTo()
```
Use:
```php
reference_type (string)
reference_id (uuid|int)
```

No Eloquent relation. Resolution happens at the service or application layer.

#### 2. Introduce a `PolymorphicRegistry`
A simple resolver class per module:
```php
resolve(string $type, string|int $id)
```
Used only at runtime (DTO / Resource layer).

#### 3. Class Map Enforcement
- Use **logical names**, not PHP class names
- Example:
```php
'post' => 'content'
'comment' => 'discussion'
```

Stored values must not depend on namespaces.

### Output of Phase 1
- Database still shared
- Modules isolated
- No hard Eloquent coupling across modules
- Polymorphism becomes **data‑driven**, not ORM‑driven

---

## Phase 2: Modular Monolith with Service Boundaries

**Goal:** Prepare polymorphic data for extraction without schema rewrites.

### Key Principles
- Polymorphism becomes **contract‑based**
- All cross‑module resolution happens via **Application Services**

### Changes

#### 1. Remove All Cross‑Module Model Imports
- No `use OtherModule\Models\X`
- Modules communicate via:
  - Interfaces
  - DTOs
  - Query Services

#### 2. Introduce Read Models
Instead of resolving polymorphic targets directly:
- Create **denormalized read tables**
- Example:
```text
activity_targets
- target_type
- target_id
- title
- metadata_json
```

Written synchronously for now.

#### 3. Polymorphism as Capability, Not Relation
Replace:
```php
$comment->commentable
```
With:
```php
$comment->target()
```
Where `target()` returns a DTO, not a Model.

### Output of Phase 2
- Polymorphism no longer ORM‑dependent
- Modules are logically service‑ready
- Database schema is future‑proof

---

## Phase 3: Microservices (Laravel per Service)

**Goal:** Eliminate polymorphic relations completely at database level.

### Key Principles
- **No cross‑service joins**
- **No polymorphic foreign keys**
- Polymorphism becomes **eventual and semantic**

### Final Transformation

#### 1. Replace Polymorphism with Events
Instead of referencing another service directly:
- Store only:
```text
subject_type
subject_id
```
- Resolve via:
  - HTTP
  - gRPC
  - Async events

#### 2. Local Projection Tables
Each service maintains its own projection:
```text
external_entities
- external_id
- external_type
- snapshot_json
```

Updated via events (Kafka / Redis / SQS).

#### 3. Contract‑First Communication
- JSON Schemas or OpenAPI
- No shared code
- No shared enums

### Output of Phase 3
- Fully decoupled services
- Polymorphism exists only as **business meaning**, not structure
- Safe independent scaling and deployment

---

## Final Rule Summary

| Stage | Polymorphism |
|-----|-------------|
| Modular Monolith | Internal only |
| Service‑Ready Modular | Data‑driven |
| Microservices | Event‑based |

---

## Golden Rule

> **If polymorphism crosses a service boundary, it is no longer a relation — it is a contract.**

