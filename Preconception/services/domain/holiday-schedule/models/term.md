### Term

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - academic_year_id (integer)
  - name_ar (string)
  - name_en (string, nullable)
  - start_date (datetime)
  - end_date (datetime)
  - is_active (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo academicYear (AcademicYear)

## External Data Dependencies

- Attendance Context
  - Required fields:
    - (via hasMany)
  - Source module: attendance-management
  - Usage: Links term to attendance records
  - Access pattern: read-only

- Subject Context
  - Required fields:
    - (via hasMany)
  - Source module: subject-grade-management
  - Usage: Links term to subject definitions
  - Access pattern: read-only

- MainSubscription Context
  - Required fields:
    - (via morphMany as period)
  - Source module: subscription-billing
  - Usage: Links term to subscription periods
  - Access pattern: read-only
- Notes:
  - Academic term/semester definition
  - Part of academic year
  - Used as subscription period
  - Should stay internal to the service
