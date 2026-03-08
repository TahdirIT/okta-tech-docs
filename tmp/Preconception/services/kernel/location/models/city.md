### City

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - region_id (integer)
  - name_ar (string)
  - name_en (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo region (Region)
  - hasMany districts (District)
  - hasMany schools (School)
- Notes:
  - Third-level geographical entity
  - Part of location hierarchy
  - Should stay internal to the service
