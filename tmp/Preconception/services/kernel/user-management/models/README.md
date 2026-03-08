# User Management — Models

## Core Model

**[User](user.md)** is the core model and aggregate root. All user-related operations and external integrations should use User as the primary entity.

## Model Hierarchy

```
                    ┌─────────┐
                    │  User   │  ← Core (aggregate root)
                    └────┬────┘
                         │
         ┌───────────────┼───────────────┐
         │               │               │
         ▼               ▼               ▼
    ┌─────────┐    ┌─────────┐    ┌──────────────┐
    │   IAM   │    │  Name   │    │   Profile    │
    │(identity)│   │(locales)│    │(user profile)│
    └────┬────┘    └─────────┘    └──────────────┘
         │
         ▼
    ┌─────────────────┐
    │ National Identity│
    └─────────────────┘
```

- **User** → IAM (belongsTo), Profile (hasOne), Name (hasMany), National Identity (via IAM)
- **IAM** — Identity, ULID, email, phone, auth. 1:1 with User.
- **Profile** — Profile data; refers to User (belongsTo User). Access via `user.profile`.
- **Name** — Localized names; belongsTo User. Access via `user.names`.
- **National Identity** — Govt ID; belongsTo IAM. Access via `user.iam.nationalIdentity`.

## Model Index

| Model | Type | Purpose |
|-------|------|---------|
| [User](user.md) | Core | Aggregate root; primary entity for APIs and consumers |
| [IAM](iam.md) | Reference | Identity, auth, ULID, email, phone |
| [Profile](profile.md) | Reference | User profile (gender, avatar, nationality, birth_date) |
| [Name](name.md) | Reference | Localized display names (ar, en, etc.) |
| [National Identity](national-id.md) | Reference | National ID hash, masked value, verification |

## Usage

Always **load User first** when working with user data. Hydrate IAM, Profile, Name, or National Identity as needed. Use `user.iam.ulid` for external identifiers.
