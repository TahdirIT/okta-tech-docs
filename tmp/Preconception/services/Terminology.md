# Architecture Terminology

This document defines the official terminology used across the system
architecture and documentation.

Its purpose is to establish a shared language and prevent ambiguity
during design, documentation, and future implementation phases.

---

## Service

A Service (or Module) represents a **business capability boundary**.
It encapsulates a coherent set of responsibilities, rules, and data
that serve a specific purpose within the system.

Services are the **only architectural units** that may evolve into
independently deployable microservices.

**Normative rule:**
> Services are extracted.  
> Models are never extracted.

---

## Module

A Module is a logical packaging unit used within a modular monolithic
architecture.

Modules:
- Represent service boundaries
- Are NOT deployment units
- Do NOT imply network isolation

A module may later be extracted into a microservice
when architectural and operational conditions allow.

---

## Model

A Model represents a **data concept owned by a single service**.
Models exist strictly within the boundary of their owning service
and must not be shared or reused directly by other services.

Models are used to express:
- Data structure
- Domain behavior
- State transitions

Models are **not** architectural or deployment boundaries.

---

## Reference Model

A Reference Model represents **shared, relatively stable data**
used primarily for classification, configuration, or lookup.

### Characteristics
- Read-heavy
- Low behavioral complexity
- Infrequent changes
- Widely consumed across services

### Examples
- Country
- Region
- City
- Education Level

**Important:**
> Reference Models do not define microservice boundaries.

---

## Operational Model

An Operational Model represents **business operations, workflows,
or stateful processes** with a clear lifecycle and business rules.

### Characteristics
- High behavioral complexity
- Frequent state changes
- Central to business workflows
- Often emits domain events

### Examples
- Attendance
- Call
- Dismissal
- Conduct Case

Operational Models indicate **business behavior**,
not deployment units.

---

## Internal Association

An Internal Association describes a logical relationship between
models **within the same service boundary**.

Internal associations:
- Are allowed
- May be documented explicitly
- Must not reference external services or modules

---

## External Data Dependency

An External Data Dependency represents a **read-only dependency**
on data owned by another service.

External data dependencies:
- Do NOT imply database relationships
- Do NOT imply ORM associations
- Do NOT allow cross-service joins
- Represent required data context only

**Key principle:**
> Services depend on data, not on databases.

---

## Domain

The Domain represents the **core business logic** of a service.
It defines business rules, policies, invariants, and domain events,
independent of technical implementation details.

The Domain must not depend on:
- Frameworks
- Databases
- APIs
- Infrastructure concerns

---

## Domain Event

A Domain Event represents a **significant business fact**
that occurred within a domain.

Domain events:
- Describe what happened
- Are immutable
- Carry no assumptions about consumers
- Do not trigger actions directly

Examples:
- AttendanceMarked
- StudentSuspended
- GradeFinalized

---

## Architectural Signal

An Architectural Signal is a **non-decisive indicator**
used to reason about system structure and future evolution.

Examples of architectural signals:
- Model classification (Reference vs Operational)
- Event frequency
- Data volatility

Architectural signals:
- Do NOT mandate architectural decisions
- Are used for evaluation, not enforcement

---

## Service Extractability Principle

A service’s suitability for extraction into a microservice
is determined by the **behavior it encapsulates**, not by
individual models.

However, the dominant model types within a service
provide strong architectural signals:

- Services dominated by Reference Models  
  → Typically remain shared modules

- Services containing Operational Models with rich behavior  
  → Potential microservice candidates (in later stages)

---

## Normative Summary

```text
Models are never extracted.
Services are extracted.
Model types are signals, not decisions.
External dependencies are data-based, not relational.
