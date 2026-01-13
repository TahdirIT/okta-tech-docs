### ExamObserver

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - committee_id (integer, nullable)
  - exam_day_period_id (integer, nullable)
  - employee_id (integer)
  - stand_by (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo committee (Committee)
  - belongsTo examDayPeriod (ExamDayPeriod)

## External Data Dependencies

- Employee Context
  - Required fields:
    - employee_id
  - Source module: employee-management
  - Usage: Identifies the employee assigned as exam observer
  - Access pattern: read-only
- Notes:
  - Exam observer/proctor assignment
  - Assigns employees to monitor exam committees
  - Should stay internal to the service
