### ExamAttendance

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - exam_subject_id (integer, nullable)
  - exam_day_period_id (integer, nullable)
  - exam_period_id (integer, nullable)
  - student_id (integer)
  - status (enum)
  - attendance_time (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo examSubject (ExamSubject)
  - belongsTo examDayPeriod (ExamDayPeriod)
  - belongsTo examPeriod (ExamPeriod)

## External Data Dependencies

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student whose exam attendance is being tracked
  - Access pattern: read-only
- Notes:
  - Student attendance for exams
  - Tracks exam attendance status
  - Should stay internal to the service
