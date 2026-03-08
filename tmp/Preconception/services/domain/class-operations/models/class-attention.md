### ClassAttention

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - class_operation_id (integer)
  - student_id (integer)
  - user_id (integer, nullable)
  - type (enum)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo classOperation (ClassOperation)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom attention is being tracked
  - Access pattern: read-only

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Identifies the user who recorded the attention
  - Access pattern: read-only
- Notes:
  - Attention/behavior tracking in classes
  - Tracks different types of attention (positive/negative)
  - Should stay internal to the service
