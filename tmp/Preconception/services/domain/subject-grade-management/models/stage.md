### Stage

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - group_level_id (integer, nullable)
  - name (string)
  - prefix (string, nullable)
  - order (integer)
  - color (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - belongsTo groupLevel (GroupLevel)
  - hasMany sections (Section)
  - hasMany committeeTables (CommitteeTable)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school to which the stage belongs
  - Access pattern: read-only
- Notes:
  - School-specific stage/grade level
  - Part of school structure (Stage -> Section)
  - Should stay internal to the service
