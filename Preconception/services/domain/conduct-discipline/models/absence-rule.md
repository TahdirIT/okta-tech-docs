### AbsenceRule

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - conduct_rules_register_id (integer)
  - marks_system_yearly (boolean, default: false)
  - dedicated_marks (decimal, nullable)
  - dedicated_marks_before_vacation (decimal, nullable)
  - allowed_days_for_excuse_submitting (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo conductRulesRegister (ConductRulesRegister)
- Notes:
  - Rules for absence procedures
  - Should stay internal to the service
