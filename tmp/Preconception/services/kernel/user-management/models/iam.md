### IAM

## Model Type
Reference Model

**Refers to User.** IAM holds identity and auth data for the **User** core. Access via `user.iam`; IAM hasOne User.

- Fields:
  - id (integer)
  - ulid (string, unique)
  - email (string, nullable, unique)
  - phone (string, nullable)
  - phone_country_id (integer, nullable)
  - password (hashed)
  - remember_token (string, nullable)
  - is_admin (boolean, default: false)
  - email_verified_at (datetime, nullable)
  - phone_verified_at (datetime, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)

- Relations:
  - hasOne user (User) — **Refers to User**; IAM exists for User via 1:1 link
  - hasOne nationalIdentity (National Identity)

## External Data Dependencies

- Country Context (phoneCountry)
  - Required fields:
    - phone_country_id
  - Source module: location
  - Usage: Identifies the country code for the phone number
  - Access pattern: read-only

- OTP Context
  - Required fields:
    - (via morphMany)
  - Source module: authentication-authorization
  - Usage: Links user to OTP records
  - Access pattern: read-only

- Role Context (primaryRoles)
  - Required fields:
    - (via employee_school pivot)
  - Source module: access-control
  - Usage: Links user to primary roles through employee assignments
  - Access pattern: read-only

- Notes:
  - Identity and Access Management model; **refers to User** — holds identity/auth for the User core.
  - Handles authentication, authorization, and access control.
  - Core security model — should stay internal to the service.
  - **Single source of truth for ULID**: Reach via `user.iam.ulid` (or `iam.ulid` when IAM is loaded directly).
  - **Email and Phone storage**: Email and phone are stored here because they're used for authentication (login, OTP, password reset, verification). They are identity/authentication concerns, not profile concerns.
