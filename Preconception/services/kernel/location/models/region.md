### Region

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
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo country (Country)
  - hasMany cities (City)
- Notes:
  - Second-level geographical entity
  - Part of location hierarchy
  - Should stay internal to the service
