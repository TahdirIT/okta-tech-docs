### User

## Model Type
Core Model

- Fields:
  - id (integer)
  - iam_id (integer)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)

- Relations:
  - belongsTo iam (IAM)
  - hasOne profile (Profile) — **Profile refers to User**; access as `user.profile`
  - hasMany names (Name)
  - National Identity — via IAM only; access as `user.iam.nationalIdentity` (National Identity belongsTo IAM)

## Role in Model Hierarchy

**User is the core model** and aggregate root for user management. All other models exist to support the User entity:

- **IAM** — Identity and access; User links to IAM via `iam_id`. IAM refers to User. ULID, email, phone, and auth data live in IAM.
- **Profile** — User profile (gender, avatar, nationality, birth_date, etc.); refers to User, reached via `user.profile`.
- **Name** — Localized display names; User hasMany Name. Query by locale for display.
- **National Identity** — Government-issued ID data; reached via `user.iam.nationalIdentity`.

APIs and other modules should treat **User** as the primary entity. Load User, then optionally hydrate IAM, Profile, Name, and National Identity as needed.

## External Data Dependencies

- All external contexts (Student, Employee, Guardian, SchoolComplex, Chat, etc.) that reference "user" or "profile" attach to the **User** aggregate (typically via IAM or Profile). See Profile and IAM models for specific dependencies.

## Access Patterns

```
// Primary: load User as entry point
user = User.find(id)

// Identity (ULID, email, phone)
user.iam.ulid
user.iam.email
user.iam.phone

// Profile (refers to User)
user.profile

// National identity (via IAM)
user.iam.nationalIdentity

// Localized names (direct)
user.names
user.names->where('locale', 'ar')->first()->name
```

## Notes

- No ULID on User; use `user.iam.ulid` for external identifiers.
- No email/phone on User; use `user.iam.email` and `user.iam.phone`.
- Minimal fields (id, iam_id, timestamps); all other user data lives in IAM, Profile, Name, or National Identity.
