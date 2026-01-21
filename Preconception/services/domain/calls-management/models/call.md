### Call

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer)
  - term_id (integer, nullable)
  - shift_id (integer, nullable)
  - student_id (integer)
  - caller_type (string)
  - caller_id (integer)
  - on_way_location_id (integer, nullable)
  - arrived_location_id (integer, nullable)
  - pick_up_location_id (integer, nullable)
  - date (date)
  - on_way_time (time, nullable)
  - arrived_time (time, nullable)
  - pickup_time (time, nullable)
  - status (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which the call is made
  - Access pattern: read-only

- Term Context
  - Required fields:
    - term_id
  - Source module: holiday-schedule
  - Usage: Links call to a specific academic term
  - Access pattern: read-only

- Shift Context
  - Required fields:
    - shift_id
  - Source module: timetable-management
  - Usage: Links call to a specific shift
  - Access pattern: read-only

- Student Context
  - Required fields:
    - student_id
  - Source module: student-management
  - Usage: Identifies the student for whom the call is made
  - Access pattern: read-only

- Guardian Context (caller)
  - Required fields:
    - caller_type
    - caller_id
  - Source module: guardian-management
  - Usage: Identifies the guardian making the call
  - Access pattern: read-only

- Location Context (onWayLocation)
  - Required fields:
    - on_way_location_id
  - Source module: location
  - Usage: Tracks guardian location when on the way
  - Access pattern: read-only

- Location Context (arrivedLocation)
  - Required fields:
    - arrived_location_id
  - Source module: location
  - Usage: Tracks guardian location upon arrival
  - Access pattern: read-only

- Location Context (pickUpLocation)
  - Required fields:
    - pick_up_location_id
  - Source module: location
  - Usage: Tracks guardian location for pickup
  - Access pattern: read-only
- Notes:
  - Guardian call-out request
  - Tracks call lifecycle (on way, arrived, picked up)
  - Location tracking for guardian movements
  - Should stay internal to the service
