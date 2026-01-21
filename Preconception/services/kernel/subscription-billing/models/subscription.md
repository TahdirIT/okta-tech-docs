### Subscription

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - service_id (integer)
  - subscriber_type (string)
  - subscriber_id (integer)
  - active (boolean, default: false)
  - balance (integer, nullable)
  - expired_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo service (Service)
  - hasMany subscriptionLogs (SubscriptionLog)
  - hasMany transactionServices (TransactionService)

## External Data Dependencies

- School/User Context (subscriber)
  - Required fields:
    - subscriber_type
    - subscriber_id
  - Source module: tenant-management, user-management
  - Usage: Identifies the school or user that has the subscription
  - Access pattern: read-only
- Notes:
  - Service-level subscriptions
  - Points-based and period-based subscriptions
  - Tracks subscription balance and expiration
  - Core subscription model - should stay internal to the service
