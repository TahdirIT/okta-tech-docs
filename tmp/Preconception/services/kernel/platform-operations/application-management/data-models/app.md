### App

## Model Type
Reference Model

- Fields:
  - id (integer)
  - code (string, unique, max: 50)
  - name (string, max: 100)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany appVersions (AppVersion)
- Notes:
  - Represents application definitions
  - Groups version information across platforms
  - Should stay internal to the service
