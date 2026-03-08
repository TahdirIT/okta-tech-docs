# [Service Name] — Models

## Document Metadata

- **Version:** 1.0
- **Status:** Draft
- **Owner:** [Team/Individual Name]
- **Last Updated:** [YYYY-MM-DD]

---

## Core Model

**[ModelName](model-name.md)** is the core model and aggregate root. All [service-related] operations and external integrations should use [ModelName] as the primary entity.

## Model Hierarchy

```
                    ┌─────────────┐
                    │  ModelName  │  ← Core (aggregate root)
                    └──────┬──────┘
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
         ▼                 ▼                 ▼
    ┌─────────┐      ┌─────────┐      ┌─────────┐
    │ Model 1 │      │ Model 2 │      │ Model 3 │
    └─────────┘      └─────────┘      └─────────┘
```

- **[ModelName]** → [Model 1] (relationship), [Model 2] (relationship), [Model 3] (relationship)
- **[Model 1]** — [Description]. [Relationship] with [ModelName].
- **[Model 2]** — [Description]. [Relationship] with [ModelName].
- **[Model 3]** — [Description]. [Relationship] with [ModelName].

## Model Index

| Model | Type | Purpose |
|-------|------|---------|
| [ModelName](model-name.md) | Core | Aggregate root; primary entity for APIs and consumers |
| [Model 1](model-1.md) | Reference | [Purpose] |
| [Model 2](model-2.md) | Reference | [Purpose] |
| [Model 3](model-3.md) | Reference | [Purpose] |

## Usage

[Describe how to use these models:]

Always **load [ModelName] first** when working with [service] data. Hydrate [Model 1], [Model 2], or [Model 3] as needed.

## Related Documentation

- [Service Description](../description.md)
- [Boundaries](../boundaries.md)
- [Business Rules](../business-rules.md)
