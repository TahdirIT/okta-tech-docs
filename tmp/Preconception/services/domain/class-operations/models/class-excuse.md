### ClassExcuse

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - class_operation_id (integer)
  - student_id (integer)
  - user_id (integer, nullable)
  - start_at (datetime, nullable)
  - end_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo classOperation (ClassOperation)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the class excuse is issued
  - Access pattern: read-only

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Identifies the user who created the excuse
  - Access pattern: read-only
- Notes:
  - Excuses for class absences
  - Time-bound excuses for class sessions
  - Should stay internal to the service
