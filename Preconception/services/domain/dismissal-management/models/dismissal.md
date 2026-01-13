### Dismissal

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - term_id (integer, nullable)
  - shift_id (integer, nullable)
  - dismissable_type (string)
  - dismissable_id (integer)
  - causer_type (string, nullable)
  - causer_id (integer, nullable)
  - tool_link_id (integer, nullable)
  - date (date)
  - time (time, nullable)
  - status (string)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which dismissal is tracked
  - Access pattern: read-only

- Term Context
  - Required fields:
    - term_id
  - Source module: holiday-schedule
  - Usage: Links dismissal to a specific academic term
  - Access pattern: read-only

- ToolLink Context
  - Required fields:
    - tool_link_id
  - Source module: reports-analytics
  - Usage: Associates dismissal record with a tool or device
  - Access pattern: read-only

- Student/Employee Context (dismissable)
  - Required fields:
    - dismissable_type
    - dismissable_id
  - Source module: student-management, employee-management
  - Usage: References the student or employee being dismissed
  - Access pattern: read-only

- Employee/User Context (causer)
  - Required fields:
    - causer_type
    - causer_id
  - Source module: employee-management, user-management
  - Usage: Identifies the employee or user who recorded or caused the dismissal
  - Access pattern: read-only
- Notes:
  - Tracks dismissal/end-of-day departure
  - Supports polymorphic dismissable (students and employees)
  - Tracks dismissal status (dismissed, excused)
  - Can be linked to tools/devices
  - Should stay internal to the service
