### MainSubscriptionDefinition

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - description (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany mainSubscriptions (MainSubscription)
- Notes:
  - Subscription plan definitions
  - Template for creating subscriptions
  - Should stay internal to the service
