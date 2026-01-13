### TimetableWaiter

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - timetable_id (integer)
  - teacher_id (integer)
  - period_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo timetable (Timetable)
  - belongsTo period (Period)

## External Data Dependencies

- Employee Context (teacher)
  - Required fields:
    - teacher_id
  - Source module: employee-management
  - Usage: Identifies the substitute teacher
  - Access pattern: read-only
- Notes:
  - Substitute teacher availability
  - Tracks which teachers can substitute in which periods
  - Should stay internal to the service
