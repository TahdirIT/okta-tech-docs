### ExamDayPeriod

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - exam_day_id (integer)
  - period_id (integer, nullable)
  - start_time (time, nullable)
  - end_time (time, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo examDay (ExamDay)

## External Data Dependencies

- Period Context
  - Required fields:
    - period_id
  - Source module: timetable-management
  - Usage: Links exam day period to a timetable period
  - Access pattern: read-only
- Notes:
  - Exam period within an exam day
  - Links exams to time periods
  - Should stay internal to the service
