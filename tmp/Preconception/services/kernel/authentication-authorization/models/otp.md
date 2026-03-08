### OTP

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - code (string)
  - data (json, nullable)
  - user_type (string)
  - user_id (integer)
  - expires_at (datetime, nullable)
  - verified_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)
## External Data Dependencies

- User/Employee/Guardian/Student Context
  - Required fields:
    - user_type
    - user_id
  - Source module: user-management, employee-management, guardian-management, student-management
  - Usage: References the user for whom the OTP is generated
  - Access pattern: read-only
- Notes:
  - Handles OTP generation and verification for authentication
  - Supports polymorphic relationship to different user types
  - Core authentication infrastructure - should stay internal to the service
