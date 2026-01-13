### StudentConductProblem

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - student_id (integer)
  - school_id (integer)
  - academic_year_id (integer)
  - conduct_problem_id (integer)
  - educational_id (integer, nullable)
  - registered_by (integer, nullable)
  - applied_procedures (json, nullable)
  - dedicated_marks (integer, nullable)
  - repetition (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo conductProblem (ConductProblem)
  - belongsTo conductEducationalProcedure (ConductEducationalProcedure)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the conduct problem is recorded
  - Access pattern: read-only

- User Context (registered_by)
  - Required fields:
    - registered_by
  - Source module: user-management
  - Usage: Identifies the user who registered the conduct problem
  - Access pattern: read-only
- Notes:
  - Individual conduct problem record for a student
  - Tracks applied procedures and marks deducted
  - Supports repetition tracking
  - Should stay internal to the service
