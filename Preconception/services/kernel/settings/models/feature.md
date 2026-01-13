### Feature

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - (Referenced by MainSubscription via features relationship)
- Notes:
  - Feature flags for subscription management
  - Used to define available features in subscriptions
  - Should stay internal to the service
