### Period

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - name (translatable)
  - order (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany timings (PeriodTiming)
  - hasMany classOperations (ClassOperation)
  - hasMany timetableWaiters (TimetableWaiter)
  - hasMany scheduleds (Scheduled)
  - hasMany waiterScheduleds (WaiterScheduled)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: school-management
  - Usage: Identifies the school for which the period is defined
  - Access pattern: read-only
- Notes:
  - Class period definition
  - Ordered periods within a school day
  - Should stay internal to the service
