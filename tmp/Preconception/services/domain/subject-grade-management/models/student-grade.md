### StudentGrade

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - student_id (integer)
  - subject_grade_distribution_id (integer)
  - group_activity_id (integer, nullable)
  - class_operation_id (integer, nullable)
  - value (decimal, nullable)
  - note (text, nullable)
  - date (date, nullable)
  - created_by (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo distribution (SubjectGradeDistribution)
  - belongsTo groupActivity (GroupGradeActivity)
  - belongsTo classOperation (ClassOperation)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the grade is recorded
  - Access pattern: read-only

- User Context (creator)
  - Required fields:
    - created_by
  - Source module: user-management
  - Usage: Identifies the user who created the grade entry
  - Access pattern: read-only
- Notes:
  - Individual student grade entry
  - Links to grade distribution and activities
  - Should stay internal to the service
