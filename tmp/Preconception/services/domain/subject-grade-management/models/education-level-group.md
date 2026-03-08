### EducationLevelGroup

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - country_id (integer)
  - name_ar (string)
  - name_en (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsToMany levels (EducationLevel) via group_level
  - hasMany schools (School)
  - hasMany groupLevels (GroupLevel)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the education level group is defined
  - Access pattern: read-only
- Notes:
  - Groups education levels (e.g., Primary, Secondary)
  - Country-specific education structure
  - Should stay internal to the service
