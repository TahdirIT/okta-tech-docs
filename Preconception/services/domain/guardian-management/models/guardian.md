### Guardian

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - user_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
- Relations:
  - hasMany representatives (Representative)

## External Data Dependencies

- User Context
  - Required fields:
    - user_id
  - Source module: user-management
  - Usage: Links guardian account to user authentication
  - Access pattern: read-only

- Student Context
  - Required fields:
    - (via guardian_student pivot)
  - Source module: student-management
  - Usage: Links guardian to their guardianees (students)
  - Access pattern: read-only

- Call Context
  - Required fields:
    - (via morphMany as caller)
  - Source module: calls-management
  - Usage: Tracks calls made by the guardian
  - Access pattern: read-only

- ToolLink Context (linker)
  - Required fields:
    - (via morphMany as linker)
  - Source module: reports-analytics
  - Usage: Links guardian to tools or devices
  - Access pattern: read-only

- NotificationReceiver Context
  - Required fields:
    - (via morphMany as receiver)
  - Source module: notifications
  - Usage: Receives notifications as a guardian
  - Access pattern: read-only
- Notes:
  - Guardian account entity
  - Links to User model for authentication
  - Manages relationships with students
  - Should stay internal to the service
