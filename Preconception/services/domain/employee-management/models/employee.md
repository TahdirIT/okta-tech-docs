### Employee

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - user_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
## External Data Dependencies

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Links employee account to user authentication
  - Access pattern: read-only

- School Context
  - Required fields:
    - (via employee_school pivot)
  - Source module: school-management
  - Usage: Links employee to assigned schools
  - Access pattern: read-only

- Role Context (primaryRoles)
  - Required fields:
    - (via employee_school pivot)
  - Source module: roles-permissions
  - Usage: Defines primary roles for employee at schools
  - Access pattern: read-only

- Role Context (customRoles)
  - Required fields:
    - (via model_has_roles pivot)
  - Source module: roles-permissions
  - Usage: Defines custom roles for employee
  - Access pattern: read-only

- Attendance Context (attendanceable)
  - Required fields:
    - (via morphMany as attendanceable)
  - Source module: attendance-management
  - Usage: Tracks employee attendance records
  - Access pattern: read-only

- Dismissal Context (dismissable)
  - Required fields:
    - (via morphMany as dismissable)
  - Source module: dismissal-management
  - Usage: Tracks employee dismissal records
  - Access pattern: read-only

- Attendance Context (causer)
  - Required fields:
    - (via morphMany as causer)
  - Source module: attendance-management
  - Usage: Tracks attendance records caused by employee
  - Access pattern: read-only

- Dismissal Context (causer)
  - Required fields:
    - (via morphMany as causer)
  - Source module: dismissal-management
  - Usage: Tracks dismissal records caused by employee
  - Access pattern: read-only

- Process Context
  - Required fields:
    - (via morphMany as causer)
  - Source module: reports-analytics
  - Usage: Links employee to process tracking
  - Access pattern: read-only

- ToolLink Context (linkable)
  - Required fields:
    - (via morphMany as linkable)
  - Source module: reports-analytics
  - Usage: Links employee to tools or devices
  - Access pattern: read-only

- ToolLink Context (linker)
  - Required fields:
    - (via morphMany as linker)
  - Source module: reports-analytics
  - Usage: Links employee as linker to tools or devices
  - Access pattern: read-only

- ClassOperation Context (teacher)
  - Required fields:
    - (via hasMany as teacher)
  - Source module: class-operations
  - Usage: Tracks class operations where employee is the teacher
  - Access pattern: read-only

- ClassOperation Context (waiter)
  - Required fields:
    - (via hasMany as waiter)
  - Source module: class-operations
  - Usage: Tracks class operations where employee is a substitute teacher
  - Access pattern: read-only

- TimetableWaiter Context
  - Required fields:
    - (via hasMany)
  - Source module: timetable-management
  - Usage: Tracks timetable waiter assignments
  - Access pattern: read-only

- TimetableAssignments Context
  - Required fields:
    - (via hasMany)
  - Source module: timetable-management
  - Usage: Tracks timetable assignments for employee
  - Access pattern: read-only

- ExamObserver Context
  - Required fields:
    - (via hasMany)
  - Source module: exam-management
  - Usage: Tracks exam observer assignments
  - Access pattern: read-only

- Notification Context (causer)
  - Required fields:
    - (via morphMany as causer)
  - Source module: notifications
  - Usage: Tracks notifications caused by employee
  - Access pattern: read-only

- NotificationReceiver Context
  - Required fields:
    - (via morphMany as receiver)
  - Source module: notifications
  - Usage: Receives notifications as an employee
  - Access pattern: read-only
- Notes:
  - Employee entity (teachers, administrators, etc.)
  - Links to User model for authentication
  - Supports multiple school assignments
  - Role-based permissions per school
  - Should stay internal to the service
