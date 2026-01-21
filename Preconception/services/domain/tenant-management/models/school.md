### School

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - subdomain (string, unique, nullable)
  - complex_id (integer, nullable)
  - country_id (integer)
  - city_id (integer, nullable)
  - district_id (integer, nullable)
  - education_level_group_id (integer, nullable)
  - state (string)
  - avatar (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo complex (SchoolComplex)
  - morphOne watsiAccount (WatsiAccount)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country where the school is located
  - Access pattern: read-only

- City Context
  - Required fields:
    - city_id
  - Source module: location
  - Usage: Identifies the city where the school is located
  - Access pattern: read-only

- District Context
  - Required fields:
    - district_id
  - Source module: location
  - Usage: Identifies the district where the school is located
  - Access pattern: read-only

- EducationLevelGroup Context
  - Required fields:
    - education_level_group_id
  - Source module: subject-grade-management
  - Usage: Links school to education level group
  - Access pattern: read-only

- TimingGroup Context
  - Required fields:
    - (via hasMany)
  - Source module: timetable-management
  - Usage: Links school to timing groups
  - Access pattern: read-only

- User Context
  - Required fields:
    - (via employees pivot)
  - Source module: user-management
  - Usage: Links users to school through employees
  - Access pattern: read-only

- Employee Context
  - Required fields:
    - (via employee_school pivot)
  - Source module: employee-management
  - Usage: Links employees to school
  - Access pattern: read-only

- Role Context
  - Required fields:
    - (via hasMany)
  - Source module: roles-permissions
  - Usage: Links school to role definitions
  - Access pattern: read-only

- Stage Context
  - Required fields:
    - (via hasMany)
  - Source module: subject-grade-management
  - Usage: Links school to stage definitions
  - Access pattern: read-only

- Section Context
  - Required fields:
    - (via hasMany)
  - Source module: subject-grade-management
  - Usage: Links school to section definitions
  - Access pattern: read-only

- Student Context
  - Required fields:
    - (via school_student pivot)
  - Source module: student-management
  - Usage: Links students to school
  - Access pattern: read-only

- Student Context (currentStudents)
  - Required fields:
    - (via active_school_id)
  - Source module: student-management
  - Usage: Identifies students with this school as their active school
  - Access pattern: read-only

- Attendance Context
  - Required fields:
    - (via hasMany)
  - Source module: attendance-management
  - Usage: Links school to attendance records
  - Access pattern: read-only

- Call Context
  - Required fields:
    - (via hasMany)
  - Source module: calls-management
  - Usage: Links school to call records
  - Access pattern: read-only

- Leave Context
  - Required fields:
    - (via hasMany)
  - Source module: leave-management
  - Usage: Links school to leave records
  - Access pattern: read-only

- Excuse Context
  - Required fields:
    - (via hasMany)
  - Source module: excuse-management
  - Usage: Links school to excuse records
  - Access pattern: read-only

- Dismissal Context
  - Required fields:
    - (via hasMany)
  - Source module: dismissal-management
  - Usage: Links school to dismissal records
  - Access pattern: read-only

- AbsenceConfirmation Context
  - Required fields:
    - (via hasMany)
  - Source module: attendance-management
  - Usage: Links school to absence confirmation records
  - Access pattern: read-only

- Device Context
  - Required fields:
    - (via morphMany)
  - Source module: file-management
  - Usage: Links school to device records
  - Access pattern: read-only

- Subject Context
  - Required fields:
    - (via hasMany)
  - Source module: subject-grade-management
  - Usage: Links school to subject definitions
  - Access pattern: read-only

- Period Context
  - Required fields:
    - (via hasMany)
  - Source module: timetable-management
  - Usage: Links school to period definitions
  - Access pattern: read-only

- Timetable Context
  - Required fields:
    - (via hasMany)
  - Source module: timetable-management
  - Usage: Links school to timetable definitions
  - Access pattern: read-only

- ExamPeriod Context
  - Required fields:
    - (via hasMany)
  - Source module: exam-management
  - Usage: Links school to exam period definitions
  - Access pattern: read-only

- Notification Context (sender)
  - Required fields:
    - (via morphMany as sender)
  - Source module: notifications
  - Usage: Links school to notifications sent
  - Access pattern: read-only

- NotificationDefinition Context
  - Required fields:
    - (via hasMany)
  - Source module: notifications
  - Usage: Links school to notification definitions
  - Access pattern: read-only

- StudentConductProblem Context
  - Required fields:
    - (via hasMany)
  - Source module: conduct-discipline
  - Usage: Links school to student conduct problem records
  - Access pattern: read-only

- ModelSettings Context
  - Required fields:
    - (via morphOne)
  - Source module: settings
  - Usage: Links school to settings
  - Access pattern: read-only

- MainSubscription Context
  - Required fields:
    - (via morphMany as subscriber)
  - Source module: subscription-billing
  - Usage: Links school to subscription records
  - Access pattern: read-only

- MainSubscriptionSetting Context
  - Required fields:
    - (via hasOne)
  - Source module: subscription-billing
  - Usage: Links school to subscription settings
  - Access pattern: read-only

- HolidaySchedule Context
  - Required fields:
    - (via morphMany)
  - Source module: holiday-schedule
  - Usage: Links school to holiday schedule records
  - Access pattern: read-only
- Notes:
  - Core school entity
  - Central to all school-related operations
  - Manages school state (active, test, inactive)
  - Should stay internal to the service
