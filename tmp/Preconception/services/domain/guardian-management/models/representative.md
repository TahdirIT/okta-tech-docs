### Representative

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - student_id (integer)
  - user_id (integer)
  - guardian_id (integer, nullable)
  - roles (enum collection, nullable)
  - status (enum)
  - start_at (date, nullable)
  - end_at (date, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo guardian (Guardian)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the representative acts
  - Access pattern: read-only

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Identifies the user who is the representative
  - Access pattern: read-only
- Notes:
  - Representative management for guardians
  - Tracks representative roles and status
  - Time-bound representative assignments
  - Should stay internal to the service
