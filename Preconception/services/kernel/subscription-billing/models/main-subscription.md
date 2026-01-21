### MainSubscription

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - main_subscription_definition_id (integer)
  - subscriber_type (string)
  - subscriber_id (integer)
  - causer_type (string, nullable)
  - causer_id (integer, nullable)
  - period_type (string, nullable)
  - period_id (integer, nullable)
  - status (string)
  - seats_count (integer, nullable)
  - additional_seats_count (integer, nullable)
  - price (decimal)
  - seat_price (decimal, nullable)
  - trial_days (integer, nullable)
  - started_at (datetime, nullable)
  - start_date (datetime, nullable)
  - end_date (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo mainSubscriptionDefinition (MainSubscriptionDefinition)
  - hasMany mainSubscriptionSettings (MainSubscriptionSetting)

## External Data Dependencies

- School/SchoolComplex Context (subscriber)
  - Required fields:
    - subscriber_type
    - subscriber_id
  - Source module: tenant-management
  - Usage: Identifies the school or school complex that has the subscription
  - Access pattern: read-only

- User Context (causer)
  - Required fields:
    - causer_type
    - causer_id
  - Source module: user-management
  - Usage: Identifies the user who caused the subscription creation
  - Access pattern: read-only

- AcademicYear/Term Context (period)
  - Required fields:
    - period_type
    - period_id
  - Source module: holiday-schedule
  - Usage: Links subscription to an academic year or term period
  - Access pattern: read-only
- Notes:
  - Main subscription entity for schools and complexes
  - Supports trial periods and seat management
  - Polymorphic subscriber and period relationships
  - Core billing model - should stay internal to the service
