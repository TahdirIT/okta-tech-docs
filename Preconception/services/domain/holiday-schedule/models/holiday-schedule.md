### HolidaySchedule

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - related_type (string)
  - related_id (integer)
  - title (translatable, nullable)
  - type (enum)
  - start_at (date)
  - end_at (date)
  - register_absent (boolean, default: false)
  - send_notifications (boolean, default: false)
  - send_notifications_at (datetime, nullable)
  - notified_users (enum collection, nullable)
  - notification_content (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
## External Data Dependencies

- Country/School Context (related)
  - Required fields:
    - related_type
    - related_id
  - Source module: location, school-management
  - Usage: Links holiday schedule to a country or school
  - Access pattern: read-only
- Notes:
  - Holiday and schedule definitions
  - Supports country-level and school-level holidays
  - Can trigger absence registration and notifications
  - Should stay internal to the service
