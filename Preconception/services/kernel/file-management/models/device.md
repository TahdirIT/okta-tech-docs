### Device

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - owner_type (string)
  - owner_id (integer)
  - name (string, nullable)
  - token (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - morphMany notificationTokens (NotificationToken)

## External Data Dependencies

- School/SchoolComplex Context (owner)
  - Required fields:
    - owner_type
    - owner_id
  - Source module: tenant-management
  - Usage: Identifies the school or school complex that owns the device
  - Access pattern: read-only
- Notes:
  - Device registration and management
  - Used for push notifications
  - Supports polymorphic ownership
  - Should stay internal to the service
