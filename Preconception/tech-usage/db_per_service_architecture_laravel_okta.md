# Database per Service Architecture

## 1. Overview
This document explains how to implement a **Database per Service** strategy within the Okta platform using the given technical stack:

- Laravel 12
- Modular Architecture (initially)
- Gradual transition to Microservices
- Independent DB connections per service
- No hard‑coded credentials
- No direct usage of `.env` inside domain modules

The goal is to achieve **strong isolation, scalability, and future portability**.

---

## 2. Why Database per Service?

### Benefits
- Strong service isolation
- Independent scaling and optimization
- Clear ownership of data
- Safer refactoring and migrations
- Easier future extraction to microservices

### Trade‑offs
- Cross‑service queries are not allowed
- Requires integration layer (API / Events)
- Higher initial architectural discipline

---

## 3. High‑Level Architecture

```
┌──────────────┐
│   Kernel     │
│──────────────│
│ Auth
│ Identity
│ Tenant
│ Config
└──────┬───────┘
       │
┌──────▼──────────────┐
│ Domain Services     │
│────────────────────│
│ School Service     │ → DB: schools_db
│ Academic Service   │ → DB: academic_db
│ Attendance Service │ → DB: attendance_db
│ Billing Service    │ → DB: billing_db
└────────────────────┘
```

Each service **owns its database completely**.

---

## 4. Connection Strategy (No .env, No Hard‑Code)

### 4.1 Centralized Connection Registry

All database credentials are resolved at runtime via:

- Secure Config Store (DB / Vault)
- Tenant‑aware resolver

Example source:
- `kernel_configurations` table
- External secrets manager (future‑ready)

---

## 5. Laravel Implementation (Modular Phase)

### 5.1 Dynamic Connection Resolver

```php
class ServiceDatabaseResolver
{
    public static function resolve(string $service): string
    {
        $config = ServiceConfig::for($service);

        config([
            "database.connections.$service" => [
                'driver'   => 'pgsql',
                'host'     => $config->host,
                'port'     => $config->port,
                'database' => $config->database,
                'username' => $config->username,
                'password' => $config->password,
            ]
        ]);

        return $service;
    }
}
```

---

### 5.2 Service‑Scoped Models

```php
class Attendance extends Model
{
    protected $connection = 'attendance_service';
}
```

Or resolved dynamically:

```php
protected function getConnectionName()
{
    return ServiceDatabaseResolver::resolve('attendance');
}
```

---

## 6. Service Boundaries Rules

### Strict Rules
- ❌ No joins across services
- ❌ No shared tables
- ❌ No foreign keys between databases

### Allowed Communication
- HTTP APIs
- Internal SDKs
- Async Events

---

## 7. Migrations Strategy

Each service owns:

```
modules/
 └── Attendance/
     ├── database/
     │   └── migrations/
     └── Models/
```

Migrations run with:

```bash
php artisan migrate --database=attendance_service
```

---

## 8. Transition to Microservices

Because each service already has:

- Independent DB
- Isolated schema
- Explicit API boundary

Extraction becomes:

```
Laravel Module → Standalone Service
```

No data migration required.

---

## 9. Security Considerations

- Credentials never stored in code
- Runtime injection only
- Per‑service DB user
- Read/Write isolation possible

---

## 10. Recommended Naming Convention

| Service | Connection | Database |
|------|-----------|----------|
| Auth | auth_service | okta_auth_db |
| Academic | academic_service | okta_academic_db |
| Attendance | attendance_service | okta_attendance_db |
| Billing | billing_service | okta_billing_db |

---

## 11. Summary

- Database per Service is fully achievable in Laravel
- Works perfectly with Modular → Microservices roadmap
- Matches Okta Kernel / Domain separation
- Future‑proof and enterprise‑grade

---

## 12. Next Steps

- Add Service Registry UI
- Implement connection caching
- Add async event bus
- Introduce secrets manager

---

**Status:** Architecture‑Approved

