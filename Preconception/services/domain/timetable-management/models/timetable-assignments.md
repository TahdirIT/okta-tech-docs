### TimetableAssignments

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - timetable_id (integer)
  - employee_id (integer)
  - subject_id (integer)
  - period_id (integer, nullable)
  - section_id (integer)
  - day (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo timetable (Timetable)
  - belongsTo period (Period)
  - hasMany scheduleds (Scheduled)

## External Data Dependencies

- Employee Context
  - Required fields:
    - employee_id
  - Source module: employee-management
  - Usage: Identifies the teacher assigned to the timetable
  - Access pattern: read-only

- Subject Context
  - Required fields:
    - subject_id
  - Source module: subject-grade-management
  - Usage: Identifies the subject being taught
  - Access pattern: read-only

- Section Context
  - Required fields:
    - section_id
  - Source module: subject-grade-management
  - Usage: Identifies the section for which the assignment is made
  - Access pattern: read-only
- Notes:
  - Teacher-subject-section-period assignments
  - Defines which teacher teaches what subject to which section
  - Should stay internal to the service
