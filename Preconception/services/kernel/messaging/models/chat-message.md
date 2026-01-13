### ChatMessage

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - chat_id (integer)
  - sender_id (integer)
  - receiver_id (integer, nullable)
  - message (text, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo chat (Chat)

## External Data Dependencies

- User Context (sender)
  - Required fields:
    - sender_id
  - Source module: user-management
  - Usage: Identifies the user who sent the message
  - Access pattern: read-only

- User Context (receiver)
  - Required fields:
    - receiver_id
  - Source module: user-management
  - Usage: Identifies the user who receives the message
  - Access pattern: read-only
- Notes:
  - Individual chat messages
  - Direct messaging between users
  - Core messaging infrastructure
  - Should stay internal to the service
