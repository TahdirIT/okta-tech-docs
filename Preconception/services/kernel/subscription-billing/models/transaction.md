### Transaction

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - subscriber_type (string)
  - subscriber_id (integer)
  - subscribable_type (string, nullable)
  - subscribable_id (integer, nullable)
  - coupon_id (integer, nullable)
  - status (enum)
  - auto_renew (boolean, default: false)
  - discount_amount (decimal, nullable)
  - next_transaction_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo coupon (Coupon)
  - hasMany transactionServices (TransactionService)
  - belongsToMany packages (Package) via transaction_package
  - morphMany subscriptionLogs (SubscriptionLog) as causer

## External Data Dependencies

- School/SchoolComplex/User Context (subscriber)
  - Required fields:
    - subscriber_type
    - subscriber_id
  - Source module: tenant-management, user-management
  - Usage: Identifies the school, school complex, or user making the transaction
  - Access pattern: read-only

- Service/Package Context (subscribable)
  - Required fields:
    - subscribable_type
    - subscribable_id
  - Source module: subscription-billing
  - Usage: References the service or package being purchased
  - Access pattern: read-only
- Notes:
  - Payment transaction entity
  - Supports VAT calculation and discount application
  - Core billing model - should stay internal to the service
