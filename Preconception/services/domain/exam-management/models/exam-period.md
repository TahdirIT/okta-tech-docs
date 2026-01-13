### ExamPeriod

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - name (string, nullable)
  - start_date (date)
  - end_date (date)
  - confirmed (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany committees (Committee)
  - hasManyThrough committeeColumns (CommitteeColumn) via committees
  - hasMany examDays (ExamDay)
  - hasManyThrough examDayPeriods (ExamDayPeriod) via examDays

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which the exam period is defined
  - Access pattern: read-only
- Notes:
  - Exam period definition
  - Groups exams within a time period
  - Should stay internal to the service
