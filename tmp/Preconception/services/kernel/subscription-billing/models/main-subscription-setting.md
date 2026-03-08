### MainSubscriptionSetting

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - main_subscription_id (integer)
  - school_id (integer)
  - settings (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo mainSubscription (MainSubscription)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which subscription settings are configured
  - Access pattern: read-only
- Notes:
  - School-specific subscription settings
  - JSON-based configuration storage
  - Should stay internal to the service
