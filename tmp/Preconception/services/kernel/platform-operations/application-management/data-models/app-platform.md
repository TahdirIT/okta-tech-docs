### AppPlatform

## Model Type
Reference Model

- Fields:
  - id (integer)
  - code (string, unique, max: 30)
  - name (string, max: 100)
  - store_url (text, nullable)
  - icon_svg (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany appVersions (AppVersion)
- Notes:
  - Represents mobile/desktop platforms (iOS, Android, Web, etc.)
  - Contains platform metadata and store information
  - Should stay internal to the service
