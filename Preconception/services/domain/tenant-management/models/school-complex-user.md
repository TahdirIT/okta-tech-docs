### SchoolComplexUser

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_complex_id (integer)
  - user_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo schoolComplex (SchoolComplex)

## External Data Dependencies

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Links user to school complex
  - Access pattern: read-only
- Notes:
  - Pivot table for complex supervisors
  - Links users to school complexes
  - Should stay internal to the service
