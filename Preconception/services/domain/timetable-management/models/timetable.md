### Timetable

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - term_id (integer, nullable)
  - name (translatable)
  - is_active (boolean, default: false)
  - waitings (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - hasMany assignments (TimetableAssignments)
  - hasMany rules (TimetableRule)
  - hasMany timetableWaiters (TimetableWaiter)
  - hasMany scheduleds (Scheduled)
  - hasMany waiterScheduleds (WaiterScheduled)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which the timetable is defined
  - Access pattern: read-only

- Term Context
  - Required fields:
    - term_id
  - Source module: holiday-schedule
  - Usage: Links timetable to a specific academic term
  - Access pattern: read-only
- Notes:
  - School timetable entity
  - Manages class schedules for a term
  - Supports active/inactive timetables
  - Should stay internal to the service
