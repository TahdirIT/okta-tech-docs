### Permission

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - guard_name (string)
  - tab_name (translatable, nullable)
  - group_name (translatable, nullable)
  - permission_name (translatable, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
## External Data Dependencies

- Service Context
  - Required fields:
    - (via permission_service pivot)
  - Source module: subscription-billing
  - Usage: Links permission to services for feature-based access control
  - Access pattern: read-only
- Notes:
  - Extends Spatie Permission model
  - Translatable permission names
  - Links permissions to services for feature-based access control
  - Core authorization model - should stay internal to the service
