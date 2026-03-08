### TimetableRule

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - timetable_id (integer)
  - ruled_type (string)
  - ruled_id (integer)
  - status (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo timetable (Timetable)

## External Data Dependencies

- Employee Context (ruled)
  - Required fields:
    - ruled_type
    - ruled_id
  - Source module: employee-management
  - Usage: References the employee for which the rule applies
  - Access pattern: read-only
- Notes:
  - Timetable optimization rules
  - Defines constraints for timetable generation
  - Should stay internal to the service
