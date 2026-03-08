# [Model Name]

## Document Metadata

- **Version:** 1.0
- **Status:** Draft
- **Owner:** [Team/Individual Name]
- **Last Updated:** [YYYY-MM-DD]

---

## Overview

[Model Name] is [description of what this model represents].

## Purpose

[Explain the purpose and role of this model in the service.]

## Attributes

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | integer | Yes | Primary key |
| `field1` | string | Yes | [Description] |
| `field2` | integer | No | [Description] |
| `field3` | datetime | No | [Description] |
| `created_at` | datetime | Yes | Creation timestamp |
| `updated_at` | datetime | Yes | Last update timestamp |

## Relationships

### Belongs To

- **[Related Model]** - [Description of relationship]

### Has One

- **[Related Model]** - [Description of relationship]

### Has Many

- **[Related Model]** - [Description of relationship]

## Business Rules

- [Business rule 1]
- [Business rule 2]
- [Business rule 3]

## Validation Rules

- [Validation rule 1]
- [Validation rule 2]

## State Transitions

[If applicable, describe state transitions:]

```
[State 1] → [Action] → [State 2]
```

## Access Patterns

[Describe common access patterns:]

- [Pattern 1]
- [Pattern 2]

## Examples

### Example 1: [Use Case]

[Description of example]

```php
// Example code or usage
```

## Related Documentation

- [Models Overview](README.md)
- [Service Description](../description.md)
- [Business Rules](../business-rules.md)
