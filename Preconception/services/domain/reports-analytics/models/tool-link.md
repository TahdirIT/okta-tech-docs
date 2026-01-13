### ToolLink

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - tool_id (integer)
  - linkable_type (string)
  - linkable_id (integer)
  - linker_type (string, nullable)
  - linker_id (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo tool (Tool)

## External Data Dependencies

- Student/Employee Context (linkable)
  - Required fields:
    - linkable_type
    - linkable_id
  - Source module: student-management, employee-management
  - Usage: References the student or employee linked to the tool
  - Access pattern: read-only

- Employee/Guardian Context (linker)
  - Required fields:
    - linker_type
    - linker_id
  - Source module: employee-management, guardian-management
  - Usage: Identifies the employee or guardian who linked the tool
  - Access pattern: read-only

- Attendance Context
  - Required fields:
    - (via hasMany)
  - Source module: attendance-management
  - Usage: Links tool to attendance records
  - Access pattern: read-only
- Notes:
  - Links tools to students/employees
  - Tracks who linked the tool
  - Should stay internal to the service
