# User Management — Design Decisions

**Core model:** [User](models/user.md) is the aggregate root. All other models (IAM, Profile, Name, National Identity) support the User entity. See [models/README](models/README.md) for the hierarchy.

## ULID Usage Strategy

**Decision: Centralize ULID in IAM model; all other models reference IAM via `iam_id` foreign key.**

### Single Source of Truth: IAM Model

- **IAM** — Only model with ULID
  - Contains the single external identifier (ULID) for the user identity
  - All other models reference IAM via `iam_id` foreign key
  - ULID is accessed via `iam.ulid` when needed

**Rationale:**
- **Single source of truth**: One place for the external identifier
- **No duplication**: ULID stored once, referenced everywhere
- **Consistency**: All external references go through IAM → ULID
- **Simpler architecture**: Clear hierarchy (IAM is the root identity)
- **Efficient**: Integer foreign keys for joins, ULID only when exposed

### Models WITHOUT ULID (Reference IAM)

- **User** — References IAM via `iam_id`
  - No ULID; get ULID via `user.iam.ulid`
  - Integer `id` for internal operations, `iam_id` for identity lookup

- **Profile** — References User via `user_id`
  - No ULID; get ULID via `user.iam.ulid` or `profile.user.iam.ulid`
  - Integer `id` for internal operations, `user_id` for user lookup

- **National Identity** — References IAM via `iam_id`
  - No ULID; internal-only model
  - Integer `id` for internal operations, `iam_id` for identity lookup

- **Name** — References User via `user_id` (which references IAM)
  - Lookup/translation table
  - Always accessed via parent relationships
  - No direct ULID needed

### Access Pattern

When you need the ULID for external exposure:
```sql
-- Get ULID via IAM
SELECT iam.ulid FROM users 
JOIN iams ON users.iam_id = iams.id 
WHERE users.id = ?

-- Or via ORM
user.iam.ulid
profile.user.iam.ulid
```

### Decision Criteria

**Centralize ULID in IAM when:**
- Multiple related models need the same external identifier
- You want a single source of truth for identity
- Models are tightly coupled (1:1 or belongsTo relationships)
- You want to avoid ULID duplication across models

**Use separate ULID per model when:**
- Models are independent entities with separate lifecycles
- Models are exposed via different APIs/URLs independently
- Models have different access patterns or security requirements

## Email and Phone Storage

**Decision: Store email and phone in IAM model, not in User or Profile.**

### Storage Location: IAM Model

- **IAM** — Contains email and phone
  - `email` (string, nullable, unique)
  - `phone` (string, nullable)
  - `phone_country_id` (integer, nullable)
  - `email_verified_at` (datetime, nullable)
  - `phone_verified_at` (datetime, nullable)

**Rationale:**
- **Authentication concern**: Email and phone are used for authentication (login, OTP, password reset, verification)
- **Identity verification**: Verification timestamps (`email_verified_at`, `phone_verified_at`) are already in IAM
- **Single source of truth**: Avoids duplication across User/Profile models
- **Security boundary**: Authentication credentials belong with IAM, not profile data
- **Consistency**: All authentication-related fields (password, email, phone, tokens) in one place

### Models WITHOUT Email/Phone

- **User** — No email/phone fields
  - Access via `user.iam.email` or `user.iam.phone` when needed

- **Profile** — No email/phone fields
  - Access via `user.iam.email` / `user.iam.phone` or `profile.user.iam.email` / `profile.user.iam.phone` when needed
  - Profile contains personal information (name, gender, avatar, birth_date, nationality), not authentication data

### Access Pattern

```php
// Get email/phone for authentication
$email = $user->iam->email;
$phone = $user->iam->phone;

// Check verification status
$isEmailVerified = $user->iam->email_verified_at !== null;
$isPhoneVerified = $user->iam->phone_verified_at !== null;
```

### Decision Criteria

**Store in IAM when:**
- Field is used for authentication/identity verification
- Field has verification timestamps (`*_verified_at`)
- Field is used for login, OTP, password reset
- Field is part of the security/identity boundary

**Store in Profile when:**
- Field is purely informational/contact data
- Field is not used for authentication
- Field is part of user's personal information display
