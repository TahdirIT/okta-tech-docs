### TimingGroup

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - name (string)
  - is_relied (boolean, default: false)
  - active (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany shifts (Shift)
  - hasMany periodTimings (PeriodTiming)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which the timing group is defined
  - Access pattern: read-only
- Notes:
  - Timing group for school schedules
  - Manages different timing configurations
  - Should stay internal to the service
