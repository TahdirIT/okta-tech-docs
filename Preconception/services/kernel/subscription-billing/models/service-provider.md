### ServiceProvider

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (string)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany services (Service)
- Notes:
  - Service provider/organization
  - Groups related services
  - Should stay internal to the service
