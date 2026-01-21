### StudentAbsenceProcedure

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - student_id (integer)
  - school_id (integer)
  - academic_year_id (integer)
  - absence_procedure_id (integer)
  - registered_by (integer, nullable)
  - applied_procedures (json, nullable)
  - manually_registered_days (json, nullable)
  - dedicated_marks (integer, nullable)
  - repetition (integer, nullable)
  - applied_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo absenceProcedure (AbsenceProcedure)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the absence procedure is applied
  - Access pattern: read-only

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which the absence procedure is applied
  - Access pattern: read-only

- AcademicYear Context
  - Required fields:
    - academic_year_id
  - Source module: holiday-schedule
  - Usage: Links absence procedure to a specific academic year
  - Access pattern: read-only

- User Context (registered_by)
  - Required fields:
    - registered_by
  - Source module: user-management
  - Usage: Identifies the user who registered the absence procedure
  - Access pattern: read-only

- Attendance Context
  - Required fields:
    - (via student_absence_procedure_attendances pivot)
  - Source module: attendance-management
  - Usage: Links absence procedures to specific attendance records
  - Access pattern: read-only
- Notes:
  - Applied absence procedures for students
  - Tracks when procedures were applied
  - Should stay internal to the service
