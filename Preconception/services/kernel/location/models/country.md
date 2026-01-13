### Country

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (translatable)
  - name_ar (string, nullable)
  - name_en (string, nullable)
  - code (string, nullable)
  - phone_code (string, nullable)
  - active (boolean, default: true)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany regions (Region)
  - hasMany academicYears (AcademicYear)
  - hasMany schools (School)
  - hasMany educationLevelGroups (EducationLevelGroup)
  - hasMany subjects (Subject)
  - hasMany conductRulesRegisters (ConductRulesRegister)
  - hasOne activeConductRulesRegister (ConductRulesRegister)
  - morphOne setting (ModelSettings)
  - morphMany holidaySchedules (HolidaySchedule)
- Notes:
  - Top-level geographical entity
  - Supports settings and holiday schedules
  - Core location data - should stay internal to the service
