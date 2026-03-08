# [Service Name] — Domain Events

## Document Metadata

- **Version:** 1.0
- **Status:** Draft
- **Owner:** [Team/Individual Name]
- **Last Updated:** [YYYY-MM-DD]

---

## Domain Events

This service publishes the following domain events to notify other services of important state changes.

### Event 1: [EventName]

**Event Type:** `[service-name].[event-name]`

**Description:** [What this event represents]

**Published When:** [Trigger condition]

**Payload:**
```json
{
  "field1": "description",
  "field2": "description",
  "field3": "description"
}
```

**Fields:**
- `field1` (type) - [Description]
- `field2` (type) - [Description]
- `field3` (type) - [Description]

**Consumers:**
- [Service 1] - [How it uses this event]
- [Service 2] - [How it uses this event]

---

### Event 2: [EventName]

**Event Type:** `[service-name].[event-name]`

**Description:** [What this event represents]

**Published When:** [Trigger condition]

**Payload:**
```json
{
  "field1": "description",
  "field2": "description"
}
```

**Fields:**
- `field1` (type) - [Description]
- `field2` (type) - [Description]

**Consumers:**
- [Service 1] - [How it uses this event]

---

## Event Flow

[Describe the event flow and relationships:]

```
[Action] → [Event 1] → [Consumer Service]
[Action] → [Event 2] → [Consumer Service]
```

---

## Event Versioning

[Describe event versioning strategy:]

- [Versioning approach]
- [Backward compatibility policy]

---

## Related Documentation

- [Boundaries](boundaries.md)
- [Business Rules](business-rules.md)
- [Models](models/README.md)
