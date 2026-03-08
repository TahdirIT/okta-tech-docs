### ExamSubject

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - exam_period_id (integer, nullable)
  - exam_day_period_id (integer, nullable)
  - subject_id (integer)
  - date (date, nullable)
  - period_id (integer, nullable)
  - start_time (time, nullable)
  - end_time (time, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo examPeriod (ExamPeriod)
  - belongsTo examDayPeriod (ExamDayPeriod)

## External Data Dependencies

- Subject Context
  - Required fields:
    - subject_id
  - Source module: subject-grade-management
  - Usage: Identifies the subject being examined
  - Access pattern: read-only

- Period Context
  - Required fields:
    - period_id
  - Source module: timetable-management
  - Usage: Links exam subject to a timetable period
  - Access pattern: read-only

- Section Context
  - Required fields:
    - (via exam_subject_section pivot)
  - Source module: subject-grade-management
  - Usage: Links exam subject to sections
  - Access pattern: read-only
- Notes:
  - Exam subject scheduling
  - Defines which subjects are examined when
  - Should stay internal to the service
