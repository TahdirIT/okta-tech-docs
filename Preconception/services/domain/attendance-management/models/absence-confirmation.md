### AbsenceConfirmation

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - attendanceable_type (string)
  - attendanceable_id (integer)
  - date (date)
  - confirmed_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which absence confirmation is tracked
  - Access pattern: read-only

- Student/Employee Context (attendanceable)
  - Required fields:
    - attendanceable_type
    - attendanceable_id
  - Source module: student-management, employee-management
  - Usage: References the student or employee whose absence is being confirmed
  - Access pattern: read-only
- Notes:
  - Tracks absence confirmations
  - Used for automated absence confirmation workflows
  - Should stay internal to the service
