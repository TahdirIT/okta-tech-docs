### AcademicYear

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - country_id (integer)
  - name_ar (string)
  - name_en (string, nullable)
  - start_date (datetime)
  - end_date (datetime)
  - is_active (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - hasMany terms (Term)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the academic year is defined
  - Access pattern: read-only

- MainSubscription Context
  - Required fields:
    - (via morphMany as period)
  - Source module: subscription-billing
  - Usage: Links academic year to subscription periods
  - Access pattern: read-only
- Notes:
  - Academic year definition
  - Country-specific academic years
  - Used as subscription period
  - Should stay internal to the service
