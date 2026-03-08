### AppVersion

## Model Type
Reference Model

- Fields:
  - id (integer)
  - app_id (integer)
  - platform_id (integer)
  - version (string, max: 20)
  - build_number (integer, nullable)
  - released_at (date)
  - expires_at (date, nullable)
  - whats_new (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo app (App)
  - belongsTo platform (Platform)
- Constraints:
  - Unique combination of app_id, platform_id, and version
  - Foreign key to apps (ON DELETE CASCADE)
  - Foreign key to platforms (ON DELETE RESTRICT)
- Notes:
  - Represents a specific version of an app for a platform
  - Tracks release dates and expiration dates
  - Supports version release notes (whats_new)
  - Should stay internal to the service
