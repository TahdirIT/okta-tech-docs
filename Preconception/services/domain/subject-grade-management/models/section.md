### Section

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - stage_id (integer)
  - name (string)
  - order (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo stage (Stage)
  - hasMany assignments (TimetableAssignments)
  - hasMany scheduleds (Scheduled)
  - hasMany classOperations (ClassOperation)
  - hasMany gradeDistribution (SubjectGradeDistribution)
  - hasMany waiterScheduleds (WaiterScheduled)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school to which the section belongs
  - Access pattern: read-only

- Student Context
  - Required fields:
    - (via section_student pivot)
  - Source module: student-management
  - Usage: Links students to section
  - Access pattern: read-only

- Student Context (currentStudents)
  - Required fields:
    - (via active_section_id)
  - Source module: student-management
  - Usage: Identifies students with this section as their active section
  - Access pattern: read-only

- ExamSubject Context
  - Required fields:
    - (via exam_subject_section pivot)
  - Source module: exam-management
  - Usage: Links exam subjects to section
  - Access pattern: read-only
- Notes:
  - Class section within a stage
  - Groups students into classes
  - Should stay internal to the service
