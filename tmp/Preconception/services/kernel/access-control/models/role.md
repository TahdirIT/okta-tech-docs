### Role

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - name_ar (string, nullable)
  - name_en (string, nullable)
  - guard_name (string)
  - country_id (integer, nullable)
  - original_role_id (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo originalRole (Role)

## External Data Dependencies

- Employee Context (primaryUsers)
  - Required fields:
    - (via employee_school pivot)
  - Source module: employee-management
  - Usage: Links role to employees as primary users
  - Access pattern: read-only

- Employee Context
  - Required fields:
    - (via employee_school pivot)
  - Source module: employee-management
  - Usage: Links role to employees
  - Access pattern: read-only
- Notes:
  - Extends Spatie Permission Role model
  - Supports hierarchical roles (original_role_id)
  - Country-specific role definitions
  - Core authorization model - should stay internal to the service
