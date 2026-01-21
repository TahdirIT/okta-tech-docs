### Excuse

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - student_id (integer)
  - issuer_type (string)
  - issuer_id (integer)
  - employee_id (integer, nullable)
  - accepted_at (datetime, nullable)
  - rejected_at (datetime, nullable)
  - reason (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - hasMany pivotAttendances (AttendanceExcuse)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which the excuse is issued
  - Access pattern: read-only

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the excuse is issued
  - Access pattern: read-only

- Employee Context (acceptingEmployee)
  - Required fields:
    - employee_id
  - Source module: employee-management
  - Usage: Identifies the employee who accepted the excuse
  - Access pattern: read-only

- Employee/Guardian Context (issuer)
  - Required fields:
    - issuer_type
    - issuer_id
  - Source module: employee-management, guardian-management
  - Usage: Identifies the employee or guardian who issued the excuse
  - Access pattern: read-only

- Attendance Context
  - Required fields:
    - (via attendance_excuse pivot)
  - Source module: attendance-management
  - Usage: Links excuse to attendance records
  - Access pattern: read-only

- Process Context
  - Required fields:
    - (via morphMany as processable)
  - Source module: reports-analytics
  - Usage: Links excuse records to process tracking
  - Access pattern: read-only
- Notes:
  - Absence excuse request
  - Supports polymorphic issuer
  - Tracks acceptance/rejection by employees
  - Can be linked to multiple attendances
  - Should stay internal to the service
