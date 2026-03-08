### ConductRulesRegister

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - country_id (integer)
  - title (translatable, nullable)
  - description (translatable, nullable)
  - active (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany conductProblemGradeGroups (ConductProblemGradeGroup)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which conduct rules are defined
  - Access pattern: read-only
- Notes:
  - Country-level conduct rules register
  - Defines conduct rules and procedures
  - Should stay internal to the service
