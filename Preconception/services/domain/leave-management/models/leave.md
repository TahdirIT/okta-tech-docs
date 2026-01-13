### Leave

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - student_id (integer)
  - issuer_type (string)
  - issuer_id (integer)
  - acceptor_type (string, nullable)
  - acceptor_id (integer, nullable)
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
  - Usage: Identifies the school for which leave is requested
  - Access pattern: read-only

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student requesting leave
  - Access pattern: read-only

- Employee/Guardian Context (issuer)
  - Required fields:
    - issuer_type
    - issuer_id
  - Source module: employee-management, guardian-management
  - Usage: Identifies the employee or guardian issuing the leave request
  - Access pattern: read-only

- Employee/User Context (acceptor)
  - Required fields:
    - acceptor_type
    - acceptor_id
  - Source module: employee-management, user-management
  - Usage: Identifies the employee or user accepting or rejecting the leave request
  - Access pattern: read-only

- Process Context
  - Required fields:
    - (via morphMany)
  - Source module: reports-analytics
  - Usage: Links leave records to process tracking
  - Access pattern: read-only
- Notes:
  - Leave request entity
  - Supports polymorphic issuer and acceptor
  - Tracks leave status (approved, rejected, pending, canceled, no-response)
  - Should stay internal to the service
