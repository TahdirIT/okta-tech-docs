### Notification

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - sender_type (string, nullable)
  - sender_id (integer, nullable)
  - causer_type (string, nullable)
  - causer_id (integer, nullable)
  - title (string)
  - body (text, nullable)
  - file (string, nullable)
  - status (string)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany receivers (NotificationReceiver)

## External Data Dependencies

- School/User/Employee Context (sender)
  - Required fields:
    - sender_type
    - sender_id
  - Source module: tenant-management, user-management, employee-management
  - Usage: Identifies the sender of the notification
  - Access pattern: read-only

- Employee/User Context (causer)
  - Required fields:
    - causer_type
    - causer_id
  - Source module: employee-management, user-management
  - Usage: Identifies the employee or user who caused the notification
  - Access pattern: read-only
- Notes:
  - Core notification entity
  - Supports polymorphic senders and causers
  - Status tracking (pending, in-progress, sent)
  - Should stay internal to the service
