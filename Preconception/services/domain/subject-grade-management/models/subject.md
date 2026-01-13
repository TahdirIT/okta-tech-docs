### Subject

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - term_id (integer, nullable)
  - group_level_id (integer, nullable)
  - country_id (integer, nullable)
  - school_id (integer, nullable)
  - subject_id (integer, nullable)
  - stage_id (integer, nullable)
  - name (translatable)
  - short_name (translatable, nullable)
  - weekly_classes (integer, nullable)
  - removable (boolean, default: false)
  - file_path (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo parentSubject (Subject)
  - hasMany childSubjects (Subject)
  - hasMany classOperations (ClassOperation)
  - hasMany assignments (TimetableAssignments)
  - hasMany gradeDistributions (SubjectGradeDistribution)
  - hasMany examSubjects (ExamSubject)

## External Data Dependencies

- Term Context
  - Required fields:
    - term_id
  - Source module: holiday-schedule
  - Usage: Links subject to a specific academic term
  - Access pattern: read-only

- EducationLevel Context
  - Required fields:
    - (via belongsToMany)
  - Source module: subject-grade-management
  - Usage: Links subject to education level
  - Access pattern: read-only

- GroupLevel Context
  - Required fields:
    - group_level_id
  - Source module: subject-grade-management
  - Usage: Links subject to group level
  - Access pattern: read-only

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the subject is defined
  - Access pattern: read-only

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which the subject is defined
  - Access pattern: read-only

- School Context (via pivot)
  - Required fields:
    - (via school_subject pivot)
  - Source module: school-management
  - Usage: Links subject to multiple schools
  - Access pattern: read-only
- Notes:
  - Subject/course definition
  - Supports hierarchical subjects (parent-child)
  - Can be country-level or school-level
  - Should stay internal to the service
