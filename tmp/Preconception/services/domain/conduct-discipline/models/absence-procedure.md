### AbsenceProcedure

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - conduct_rules_register_id (integer)
  - title (translatable)
  - days (integer, nullable)
  - continuous_absences (boolean, default: false)
  - procedures (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo conductRulesRegister (ConductRulesRegister)
- Notes:
  - Absence-related disciplinary procedures
  - Should stay internal to the service
