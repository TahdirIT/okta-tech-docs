### Student

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - user_id (integer)
  - active_school_id (integer, nullable)
  - active_section_id (integer, nullable)
  - active_status (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
## External Data Dependencies

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Links student account to user authentication
  - Access pattern: read-only

- Guardian Context
  - Required fields:
    - (via guardian_student pivot)
  - Source module: guardian-management
  - Usage: Links student to guardians
  - Access pattern: read-only

- School Context
  - Required fields:
    - (via school_student pivot)
  - Source module: tenant-management
  - Usage: Links student to schools
  - Access pattern: read-only

- School Context (activeSchool)
  - Required fields:
    - active_school_id
  - Source module: tenant-management
  - Usage: Identifies the student's active school
  - Access pattern: read-only

- Section Context
  - Required fields:
    - (via section_student pivot)
  - Source module: subject-grade-management
  - Usage: Links student to sections
  - Access pattern: read-only

- Section Context (activeSection)
  - Required fields:
    - active_section_id
  - Source module: subject-grade-management
  - Usage: Identifies the student's active section
  - Access pattern: read-only

- Attendance Context
  - Required fields:
    - (via morphMany as attendanceable)
  - Source module: attendance-management
  - Usage: Tracks student attendance records
  - Access pattern: read-only

- Dismissal Context
  - Required fields:
    - (via morphMany as dismissable)
  - Source module: dismissal-management
  - Usage: Tracks student dismissal records
  - Access pattern: read-only

- Excuse Context
  - Required fields:
    - (via hasMany)
  - Source module: excuse-management
  - Usage: Links student to excuse records
  - Access pattern: read-only

- Leave Context
  - Required fields:
    - (via hasMany)
  - Source module: leave-management
  - Usage: Links student to leave records
  - Access pattern: read-only

- Call Context
  - Required fields:
    - (via hasMany)
  - Source module: calls-management
  - Usage: Links student to call records
  - Access pattern: read-only

- Representative Context
  - Required fields:
    - (via hasMany)
  - Source module: guardian-management
  - Usage: Links student to representative records
  - Access pattern: read-only

- ClassAttention Context
  - Required fields:
    - (via hasMany)
  - Source module: class-operations
  - Usage: Links student to class attention records
  - Access pattern: read-only

- ClassOperation Context
  - Required fields:
    - (via class_attendances pivot)
  - Source module: class-operations
  - Usage: Links student to class attendance records
  - Access pattern: read-only

- ClassExcuse Context
  - Required fields:
    - (via hasMany)
  - Source module: class-operations
  - Usage: Links student to class excuse records
  - Access pattern: read-only

- ConductProblem Context
  - Required fields:
    - (via student_conduct_problems pivot)
  - Source module: conduct-discipline
  - Usage: Links student to conduct problem records
  - Access pattern: read-only

- StudentConductProblem Context
  - Required fields:
    - (via hasMany)
  - Source module: conduct-discipline
  - Usage: Links student to student conduct problem records
  - Access pattern: read-only

- StudentAbsenceProcedure Context
  - Required fields:
    - (via hasMany)
  - Source module: conduct-discipline
  - Usage: Links student to absence procedure records
  - Access pattern: read-only

- Scheduled Context
  - Required fields:
    - (via active_section_id)
  - Source module: class-operations
  - Usage: Links student to scheduled classes via active section
  - Access pattern: read-only

- CommitteeTable Context
  - Required fields:
    - (via hasMany)
  - Source module: exam-management
  - Usage: Links student to committee table records
  - Access pattern: read-only

- ExamAttendance Context
  - Required fields:
    - (via hasMany)
  - Source module: exam-management
  - Usage: Links student to exam attendance records
  - Access pattern: read-only

- NotificationReceiver Context
  - Required fields:
    - (via morphMany as receiver)
  - Source module: notifications
  - Usage: Receives notifications as a student
  - Access pattern: read-only

- ToolLink Context
  - Required fields:
    - (via morphMany as linkable)
  - Source module: reports-analytics
  - Usage: Links student to tools or devices
  - Access pattern: read-only
- Notes:
  - Core student entity
  - Tracks active school and section
  - Supports student status (regular, affiliate)
  - Should stay internal to the service
