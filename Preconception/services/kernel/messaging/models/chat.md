### Chat

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - school_id (integer, nullable)
  - creator_id (integer)
  - name (string, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany messages (ChatMessage)

## External Data Dependencies

- School Context
  - Required fields:
    - school_id
  - Source module: tenant-management
  - Usage: Identifies the school for which the chat is created
  - Access pattern: read-only

- User Context (creator)
  - Required fields:
    - creator_id
  - Source module: user-management
  - Usage: Identifies the user who created the chat
  - Access pattern: read-only

- User Context
  - Required fields:
    - (via chat_user pivot)
  - Source module: user-management
  - Usage: Links users to the chat conversation
  - Access pattern: read-only
- Notes:
  - Chat room/group management
  - School-scoped chats
  - Multi-user chat support
  - Should stay internal to the service
