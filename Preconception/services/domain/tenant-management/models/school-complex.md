### SchoolComplex

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - subdomain (string, unique, nullable)
  - avatar (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany schools (School)

## External Data Dependencies

- User Context (supervisors)
  - Required fields:
    - (via school_complex_user pivot)
  - Source module: user-management
  - Usage: Links supervisors to school complex
  - Access pattern: read-only

- User Context
  - Required fields:
    - (via school_complex_user pivot)
  - Source module: user-management
  - Usage: Links users to school complex
  - Access pattern: read-only

- Device Context
  - Required fields:
    - (via morphMany)
  - Source module: file-management
  - Usage: Links devices to school complex
  - Access pattern: read-only

- MainSubscription Context
  - Required fields:
    - (via morphMany as subscriber)
  - Source module: subscription-billing
  - Usage: Links school complex to subscription records
  - Access pattern: read-only
- Notes:
  - Educational complex/group of schools
  - Manages multiple schools under one complex
  - Should stay internal to the service
