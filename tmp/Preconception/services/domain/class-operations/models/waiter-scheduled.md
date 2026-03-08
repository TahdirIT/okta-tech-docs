### WaiterScheduled

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - timetable_id (integer)
  - scheduled_id (integer, nullable)
  - section_id (integer)
  - period_id (integer, nullable)
  - teacher_id (integer)
  - day (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo scheduled (Scheduled)

## External Data Dependencies

- Timetable Context
  - Required fields:
    - timetable_id
  - Source module: timetable-management
  - Usage: Links waiter schedule to the timetable definition
  - Access pattern: read-only

- Section Context
  - Required fields:
    - section_id
  - Source module: subject-grade-management
  - Usage: Identifies the section for which the waiter is scheduled
  - Access pattern: read-only

- Period Context
  - Required fields:
    - period_id
  - Source module: timetable-management
  - Usage: Links waiter schedule to a specific period
  - Access pattern: read-only

- Employee Context (teacher)
  - Required fields:
    - teacher_id
  - Source module: employee-management
  - Usage: Identifies the substitute teacher
  - Access pattern: read-only
- Notes:
  - Substitute teacher scheduling
  - Tracks backup teachers for scheduled classes
  - Should stay internal to the service
