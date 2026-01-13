### Attendance

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - term_id (integer, nullable)
  - shift_id (integer, nullable)
  - attendanceable_type (string)
  - attendanceable_id (integer)
  - causer_type (string, nullable)
  - causer_id (integer, nullable)
  - tool_link_id (integer, nullable)
  - date (date)
  - time (time, nullable)
  - status (string)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - hasOne excuse (AttendanceExcuse)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which attendance is tracked
  - Access pattern: read-only

- Term Context
  - Required fields:
    - term_id
  - Source module: holiday-schedule
  - Usage: Links attendance to a specific academic term
  - Access pattern: read-only

- ToolLink Context
  - Required fields:
    - tool_link_id
  - Source module: reports-analytics
  - Usage: Associates attendance record with a tool or device
  - Access pattern: read-only

- Student/Employee Context (attendanceable)
  - Required fields:
    - attendanceable_type
    - attendanceable_id
  - Source module: student-management, employee-management
  - Usage: References the student or employee whose attendance is being tracked
  - Access pattern: read-only

- Employee/User Context (causer)
  - Required fields:
    - causer_type
    - causer_id
  - Source module: employee-management, user-management
  - Usage: Identifies the employee or user who recorded or caused the attendance entry
  - Access pattern: read-only

- Excuse Context
  - Required fields:
    - (via attendance_excuse pivot)
  - Source module: excuse-management
  - Usage: Links attendance records to excuse records
  - Access pattern: read-only
- Notes:
  - Core attendance tracking entity
  - Supports polymorphic attendanceable (students and employees)
  - Tracks attendance status (present, absent, late, early, etc.)
  - Can be linked to tools/devices
  - Should stay internal to the service
