### StudentAbsenceProcedureAttendance

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - s_a_procedure_id (integer)
  - attendance_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo studentAbsenceProcedure (StudentAbsenceProcedure)

## External Data Dependencies

- Attendance Context
  - Required fields:
    - attendance_id
  - Source module: attendance-management
  - Usage: Links absence procedure to a specific attendance record
  - Access pattern: read-only
- Notes:
  - Links absence procedures to specific attendances
  - Should stay internal to the service
