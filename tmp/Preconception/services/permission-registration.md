# Service Permission Registration Guide

## Audience
This document is intended for **service developers** who:
- build or maintain a service within the platform
- need to declare permissions owned by their service
- are responsible for registering permissions during deployment

---

## Purpose
Each service must explicitly declare the permissions it owns.
These permissions are registered centrally in **access-control** and later used for:
- role composition
- authorization decisions
- audit and governance

Permissions are treated as **contracts**, not implementation details.

---

## Quick Reference

| Item | Value |
|------|--------|
| File | `/<service-root>/permissions.yaml` |
| Format | `<feature>.<resource>.<action>` |
| Case | All lowercase, dot-separated |
| Wildcards | Not allowed |
| Change after registration | Not allowed |

---

## Core Principles

1. Permissions are **owned by a single logical service**
2. Permissions are **declared by the service**, not defined ad-hoc in code
3. Permission names are **human-readable and deterministic**
4. Prefixes are enforced centrally — **do not add them manually**
5. Once registered, a permission **must not be modified or reused**

---

## Permission Ownership Model

In this platform:

- Each major capability (e.g. `app`, `user`, `access`) is a **feature**
- Permissions are scoped by **feature**, **resource**, and **action**

Permission structure:

```
<feature>.<resource>.<action>
```

Examples:
```
app.application.register
app.version.create
app.version.release
app.platform.attach
```

---

## Declaring Permissions

Each service must include a `permissions.yaml` file at its root.

### File Location
```
/<service-root>/permissions.yaml
```

---

## permissions.yaml Structure

### Basic Schema

```yaml
permissions:
  - name: app.application.register
    description: Register a new application

  - name: app.version.create
    description: Create a new application version

  - name: app.version.release
    description: Release an application version

  - name: app.platform.attach
    description: Attach a platform to an application
```

**Rules:** All `name` values must be unique within the file. Duplicate names cause validation failure.

---

## Field Definitions

### `permissions[].name`
- Local permission identifier
- Must follow the format:

```
<feature>.<resource>.<action>
```

Rules:
- All lowercase
- Dot-separated
- No wildcards
- No random identifiers

---

### `permissions[].description`
- Human-readable explanation
- Used in dashboards, audits, and reviews
- Required

---

## Naming Rules (Strict)

### Feature
- Represents a major governance domain
- Examples: `app`, `user`, `access`

### Resource
- A real domain object
- Examples: `application`, `version`, `platform`

### Action
- A precise verb
- Use: `create`, `register`, `attach`, `release`, `expire`
- Avoid: `add`, `manage`, `do`

### Invalid Examples

| Invalid | Reason |
|--------|--------|
| `app.version.*` | Wildcards not allowed |
| `App.Version.Release` | Must be all lowercase |
| `app_version_release` | Use dots, not underscores |
| `app.v1.create` | Resource should be a domain object, not version identifiers |
| `app.version.add` | Prefer `create` or `register` over vague verbs |
| `app.version.manage` | Too broad; use specific actions |

---

## Registration Process

1. CI/CD pipeline reads `permissions.yaml`
2. Permissions are sent to `access-control`
3. Validation is performed:
   - **ownership** — service is allowed to own the declared feature/resource
   - **naming rules** — format and vocabulary comply with this guide
   - **uniqueness** — no duplicate names within the file or across the platform
4. Valid permissions are registered
5. **On conflict or validation failure:** deployment fails; fix `permissions.yaml` and redeploy

**Idempotency:** Re-deploying with the same, unchanged permissions is safe. Re-registration does not create duplicates.

---

## Runtime Usage

Inside your service:

- Always check permissions by **full permission name**
- Example:
```
Required permission: app.version.release
```

Do not:
- Construct permission strings dynamically
- Bypass access-control checks

---

## Common Mistakes

| Mistake | Avoid | Prefer |
|--------|--------|--------|
| Treating permissions as secrets | Storing in vault, obfuscating | Declare in `permissions.yaml`; access-control handles enforcement |
| Using random identifiers | `app.xyz7a2.create` | `app.version.create` |
| Sharing permissions across features | `common.thing.manage` used by multiple services | Each feature owns its permissions |
| Encoding repo structure | `svc-app-mgmt.version.release` | `app.version.release` |
| Modifying registered permissions | Renaming or changing semantics | Introduce new permission; deprecate old via process |
| Constructing names dynamically | Building permission strings from variables (e.g. `${feature}.${resource}.${action}`) | Use full permission names from config or constants |

---

## Troubleshooting

| Issue | Check |
|-------|--------|
| Deployment fails at permission registration | Validation errors in pipeline logs; fix naming, uniqueness, or ownership |
| Permission not found at runtime | Ensure it is in `permissions.yaml` and deployment succeeded |
| Duplicate permission error | Remove duplicate `name` in `permissions.yaml` or resolve cross-service conflict |

---

## Final Rule

> **Permissions describe intent and authority.  
> They are part of the platform contract.**
