### NotificationReceiver

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - notification_id (integer)
  - receiver_type (string)
  - receiver_id (integer)
  - read_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo notification (Notification)

## External Data Dependencies

- Student/Employee/Guardian/User Context (receiver)
  - Required fields:
    - receiver_type
    - receiver_id
  - Source module: student-management, employee-management, guardian-management, user-management
  - Usage: Identifies the recipient of the notification
  - Access pattern: read-only
- Notes:
  - Tracks notification delivery to recipients
  - Supports polymorphic receivers
  - Read status tracking
  - Should stay internal to the service
