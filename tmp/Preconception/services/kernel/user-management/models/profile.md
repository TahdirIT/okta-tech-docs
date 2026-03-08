### Profile

## Model Type
Reference Model

**Refers to User.** Profile holds user profile data for the **User** core. Access via `user.profile`; Profile belongsTo User.

- Fields:
  - id (integer)
  - user_id (integer)
  - gender (string, nullable)
  - avatar (string, nullable)
  - nationality_id (integer, nullable)
  - birth_date (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)

- Relations:
  - belongsTo user (User) — **Refers to User**; access via `user.profile`

## External Data Dependencies

- Country Context (nationality)
  - Required fields:
    - nationality_id
  - Source module: location
  - Usage: Identifies the user's nationality
  - Access pattern: read-only

- Student Context
  - Required fields:
    - (via hasOne)
  - Source module: student-management
  - Usage: Links user to student account
  - Access pattern: read-only

- Employee Context
  - Required fields:
    - (via hasOne)
  - Source module: employee-management
  - Usage: Links user to employee account
  - Access pattern: read-only

- Guardian Context
  - Required fields:
    - (via hasOne)
  - Source module: guardian-management
  - Usage: Links user to guardian account
  - Access pattern: read-only

- SchoolComplexUser Context (supervisor)
  - Required fields:
    - (via hasOne)
  - Source module: tenant-management
  - Usage: Links user to school complex supervisor role
  - Access pattern: read-only

- SchoolComplexUser Context
  - Required fields:
    - (via hasMany)
  - Source module: tenant-management
  - Usage: Links user to school complexes
  - Access pattern: read-only

- Representative Context
  - Required fields:
    - (via hasMany)
  - Source module: guardian-management
  - Usage: Links user to representative records
  - Access pattern: read-only

- Student Context (guardianees)
  - Required fields:
    - (via guardian_student pivot)
  - Source module: student-management
  - Usage: Links user as guardian to students
  - Access pattern: read-only

- Student Context (representativeStudents)
  - Required fields:
    - (via representatives)
  - Source module: student-management
  - Usage: Links user as representative to students
  - Access pattern: read-only

- Chat Context
  - Required fields:
    - (via chat_user pivot)
  - Source module: messaging
  - Usage: Links user to chat conversations
  - Access pattern: read-only

- Chat Context (createdChats)
  - Required fields:
    - (via hasMany)
  - Source module: messaging
  - Usage: Links user to chats they created
  - Access pattern: read-only

- ChatMessage Context
  - Required fields:
    - (via hasMany)
  - Source module: messaging
  - Usage: Links user to chat messages they sent
  - Access pattern: read-only

- Process Context
  - Required fields:
    - (via morphMany as causer)
  - Source module: reports-analytics
  - Usage: Links user to process records they caused
  - Access pattern: read-only

- NotificationToken Context
  - Required fields:
    - (via morphMany)
  - Source module: notifications
  - Usage: Links user to notification tokens
  - Access pattern: read-only

- MainSubscription Context
  - Required fields:
    - (via morphMany as causer)
  - Source module: subscription-billing
  - Usage: Links user to subscription records they caused
  - Access pattern: read-only

- Notes:
  - User profile information model; **refers to User** — profile data for the User core.
  - Contains personal and contact information (name, gender, avatar, birth_date, nationality).
  - Supports multiple account types through polymorphic relationships.
  - Should stay internal to the service as it's the foundation for all user-related operations.
  - No ULID: references User via `user_id`; get ULID via `user.iam.ulid` or `profile.user.iam.ulid` when needed for external exposure.
  - Email and phone are stored in IAM (not here) because they're authentication/identity concerns, not profile concerns.
