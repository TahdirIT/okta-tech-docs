### ConductProblem

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - conduct_problem_grade_id (integer)
  - title (translatable)
  - description (translatable, nullable)
  - can_be (boolean, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo conductProblemGrade (ConductProblemGrade)

## External Data Dependencies

- Student Context
  - Required fields:
    - (via student_conduct_problems pivot)
  - Source module: student-management
  - Usage: Links conduct problems to students
  - Access pattern: read-only
- Notes:
  - Conduct problem definition
  - Part of conduct rules register
  - Should stay internal to the service
