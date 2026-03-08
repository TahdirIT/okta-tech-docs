### SubjectGradeDistribution

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - subject_id (integer)
  - section_id (integer, nullable)
  - group_level_id (integer, nullable)
  - original_id (integer, nullable)
  - teacher_id (integer, nullable)
  - term_id (integer, nullable)
  - title (translatable)
  - group (boolean, default: false)
  - method (string, nullable)
  - amount (decimal, nullable)
  - link_to (string, nullable)
  - removable (boolean, default: false)
  - data (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo subject (Subject)
  - belongsTo section (Section)
  - belongsTo groupLevel (GroupLevel)
  - belongsTo originalDistribution (SubjectGradeDistribution)
  - hasMany derivedDistributions (SubjectGradeDistribution)

## External Data Dependencies

- User Context (teacher)
  - Required fields:
    - teacher_id
  - Source module: user-management
  - Usage: Identifies the teacher who created the grade distribution
  - Access pattern: read-only
- Notes:
  - Grade distribution/category definition
  - Defines how grades are structured (quizzes, exams, assignments, etc.)
  - Supports hierarchical distributions (original-derived)
  - Should stay internal to the service
