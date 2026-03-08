### ClassAttendance

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - class_operation_id (integer)
  - student_id (integer)
  - user_id (integer, nullable)
  - late (boolean, default: false)
  - present (boolean, default: false)
  - date (date, nullable)
  - time (time, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo classOperation (ClassOperation)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student whose class attendance is being tracked
  - Access pattern: read-only

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Identifies the user who recorded the attendance
  - Access pattern: read-only
- Notes:
  - Pivot table for class-level attendance
  - Tracks student presence in specific class sessions
  - Supports late tracking
  - Should stay internal to the service
