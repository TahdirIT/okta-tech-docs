### ClassOperation

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - scheduled_id (integer, nullable)
  - section_id (integer)
  - period_id (integer, nullable)
  - teacher_id (integer)
  - subject_id (integer)
  - waiter_id (integer, nullable)
  - waiter_scheduled_id (integer, nullable)
  - date (date)
  - day (string, nullable)
  - lecture_topic (string, nullable)
  - lecture_description (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo scheduled (Scheduled)
  - belongsTo waiterScheduled (WaiterScheduled)
  - hasMany attendances (ClassAttendance)
  - hasMany classExcuses (ClassExcuse)
  - hasMany classAttentions (ClassAttention)

## External Data Dependencies

- Section Context
  - Required fields:
    - section_id
  - Source module: subject-grade-management
  - Usage: Identifies the class section for which the operation is performed
  - Access pattern: read-only

- Period Context
  - Required fields:
    - period_id
  - Source module: timetable-management
  - Usage: Links class operation to a specific period
  - Access pattern: read-only

- Employee Context (teacher)
  - Required fields:
    - teacher_id
  - Source module: employee-management
  - Usage: Identifies the teacher conducting the class
  - Access pattern: read-only

- Subject Context
  - Required fields:
    - subject_id
  - Source module: subject-grade-management
  - Usage: Identifies the subject being taught in this class operation
  - Access pattern: read-only

- Employee Context (waiter)
  - Required fields:
    - waiter_id
  - Source module: employee-management
  - Usage: Identifies substitute teacher if applicable
  - Access pattern: read-only

- Student Context
  - Required fields:
    - (via class_attendances pivot)
  - Source module: student-management
  - Usage: Links students to class attendance records
  - Access pattern: read-only
- Notes:
  - Actual class session execution
  - Links scheduled classes to actual class operations
  - Tracks teacher, subject, and section
  - Supports substitute teachers (waiter)
  - Should stay internal to the service
