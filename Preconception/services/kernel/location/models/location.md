### Location

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string, nullable)
  - latitude (decimal, nullable)
  - longitude (decimal, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - (Referenced by Call model for on_way_location_id, arrived_location_id, pick_up_location_id)
- Notes:
  - GPS coordinates for location tracking
  - Used in calls management for tracking guardian locations
  - Should stay internal to the service
