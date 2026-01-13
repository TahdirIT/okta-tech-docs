### Process

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - processable_type (string)
  - processable_id (integer)
  - causer_type (string, nullable)
  - causer_id (integer, nullable)
  - data (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
## External Data Dependencies

- Leave/Excuse Context (processable)
  - Required fields:
    - processable_type
    - processable_id
  - Source module: leave-management, excuse-management
  - Usage: References the leave or excuse record being processed
  - Access pattern: read-only

- User/Employee/Guardian Context (causer)
  - Required fields:
    - causer_type
    - causer_id
  - Source module: user-management, employee-management, guardian-management
  - Usage: Identifies the user, employee, or guardian who caused the process action
  - Access pattern: read-only
- Notes:
  - Audit trail for business processes
  - Tracks workflow steps and approvals
  - Used for reporting and analytics
  - Should stay internal to the service
