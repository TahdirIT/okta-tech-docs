### NotificationDefinition

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - slug (string)
  - group_name (translatable, nullable)
  - title (translatable, nullable)
  - variables (json, nullable)
  - specifiable (boolean, default: false)
  - specified (json, nullable)
  - country_id (integer, nullable)
  - school_id (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo original (NotificationDefinition)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the notification definition is defined
  - Access pattern: read-only

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which the notification definition is defined
  - Access pattern: read-only
- Notes:
  - Template definitions for notifications
  - Supports hierarchical definitions (platform -> country -> school)
  - Customizable notification templates
  - Should stay internal to the service
