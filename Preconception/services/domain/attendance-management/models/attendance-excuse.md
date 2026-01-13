### AttendanceExcuse

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - attendance_id (integer)
  - excuse_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo attendance (Attendance)

## External Data Dependencies

- Excuse Context
  - Required fields:
    - excuse_id
  - Source module: excuse-management
  - Usage: Links attendance excuse record to the excuse entity
  - Access pattern: read-only
- Notes:
  - Pivot table linking attendances to excuses
  - Tracks which attendances are excused
  - Should stay internal to the service
