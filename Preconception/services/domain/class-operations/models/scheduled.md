### Scheduled

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - timetable_id (integer)
  - assignment_id (integer)
  - section_id (integer)
  - period_id (integer, nullable)
  - day (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany classOperations (ClassOperation)
  - hasMany waiters (WaiterScheduled)

## External Data Dependencies

- Timetable Context
  - Required fields:
    - timetable_id
  - Source module: timetable-management
  - Usage: Links scheduled class to the timetable definition
  - Access pattern: read-only

- TimetableAssignments Context
  - Required fields:
    - assignment_id
  - Source module: timetable-management
  - Usage: Links scheduled class to the timetable assignment
  - Access pattern: read-only

- Section Context
  - Required fields:
    - section_id
  - Source module: subject-grade-management
  - Usage: Identifies the section for which the class is scheduled
  - Access pattern: read-only

- Period Context
  - Required fields:
    - period_id
  - Source module: timetable-management
  - Usage: Links scheduled class to a specific period
  - Access pattern: read-only

- PeriodTiming Context
  - Required fields:
    - period_id
    - day
  - Source module: timetable-management
  - Usage: Provides timing information for the scheduled class
  - Access pattern: read-only
- Notes:
  - Scheduled class sessions from timetable
  - Links timetable assignments to specific periods and days
  - Should stay internal to the service
