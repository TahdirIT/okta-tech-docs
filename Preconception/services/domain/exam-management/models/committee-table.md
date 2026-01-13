### CommitteeTable

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - committee_column_id (integer)
  - student_id (integer, nullable)
  - stage_id (integer, nullable)
  - order (integer)
  - reservable (boolean, default: true)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo committeeColumn (CommitteeColumn)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student assigned to the committee table
  - Access pattern: read-only

- Stage Context
  - Required fields:
    - stage_id
  - Source module: subject-grade-management
  - Usage: Identifies the stage for the committee table
  - Access pattern: read-only
- Notes:
  - Individual seat/table in exam committee
  - Assigns students to specific seats
  - Should stay internal to the service
