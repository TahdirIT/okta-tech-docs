### NotificationToken

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - notifiable_type (string)
  - notifiable_id (integer)
  - token (string)
  - created_at (timestamp)
  - updated_at (timestamp)
## External Data Dependencies

- User/Device Context (notifiable)
  - Required fields:
    - notifiable_type
    - notifiable_id
  - Source module: user-management, file-management
  - Usage: References the user or device that can receive notifications
  - Access pattern: read-only
- Notes:
  - FCM push notification tokens
  - Supports polymorphic notifiables (users and devices)
  - Core infrastructure for push notifications
  - Should stay internal to the service
