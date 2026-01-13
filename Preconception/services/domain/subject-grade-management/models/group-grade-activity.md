### GroupGradeActivity

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - subject_grade_distribution_id (integer)
  - section_id (integer)
  - title (string)
  - description (text, nullable)
  - max_score (decimal, nullable)
  - date (date, nullable)
  - created_by (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo distribution (SubjectGradeDistribution)
  - belongsTo section (Section)
  - hasMany studentGrades (StudentGrade)

## External Data Dependencies

- User Context (creator)
  - Required fields:
    - created_by
  - Source module: user-management
  - Usage: Identifies the user who created the group grade activity
  - Access pattern: read-only
- Notes:
  - Group activity for grading (e.g., group project, group quiz)
  - Links multiple students to a single grade entry
  - Should stay internal to the service
