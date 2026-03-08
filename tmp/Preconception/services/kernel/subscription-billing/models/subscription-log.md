### SubscriptionLog

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - subscription_id (integer)
  - causer_type (string, nullable)
  - causer_id (integer, nullable)
  - type (enum)
  - points (integer, nullable)
  - days (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo subscription (Subscription)

## External Data Dependencies

- Transaction Context
  - Required fields:
    - causer_type
    - causer_id
  - Source module: subscription-billing
  - Usage: References the transaction that caused the subscription log entry
  - Access pattern: read-only
- Notes:
  - Audit log for subscription changes
  - Tracks deposits and withdrawals
  - Should stay internal to the service
