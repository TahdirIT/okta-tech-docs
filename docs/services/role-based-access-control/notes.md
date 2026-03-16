- `spatie/laravel-multitenancy` uses single database.
- Teams in `spatie/laravel-permission` reepresents tenants in `spatie/laravel-multitenancy` and this is managed within Middleware.
- Each permission or role has a title (ar/en + nullable) viewed for users (not the code).
- Each permission or role should has tenant id if it is in tenant scope.
- Each permission or role related to user should has tenant id if it is in tenant scope.
- The 'settings/permissions' and 'settings/roles' pages have a field to add title for permissions/roles names as additional, with migration in permissions and roles to add titles.
- Two scopes of roles/permissions: system or tenant:
  - The system scope includes the one fixed role: `superadmin`. Other system roles can be added dynamically as needed by the user has `superadmin` role.
  - The tenant scope includes the fixed roles: `admin` (who owns the tenant account), `teacher`, and `student`,  . Other system roles can be added dynamically as needed by the same user has `admin` role.
- If user has not selected a role, will redirect to `auth/context` to select a role (shows any role has whether the scope of system roles or the scope of tenants' roles, each role represents a button with the title of that role).
- Middleware: 
  - if tenant is set from `spatie/laravel-multitenancy`? set team from `spatie/laravel-permission`: else? remove team from `spatie/laravel-permission`.
  - if tenant changed? forgetCachedPermission
- Add needing seeder.

## Considerations Before Implementation

- **Package Installation**: The project currently uses a custom `Tenant` model with session-based context management. If using `spatie/laravel-multitenancy`, it needs to be installed and configured. Alternatively, the middleware should integrate with the existing custom tenant implementation to set team IDs.

- **Teams Configuration**: `config/permission.php` currently has `'teams' => false`. This needs to be changed to `'teams' => true` before running migrations that add team fields.

- **Model Configuration**: `config/permission.php` currently references default Spatie models (`Spatie\Permission\Models\Permission::class` and `Spatie\Permission\Models\Role::class`). Should be updated to use custom models (`App\Models\Permission::class` and `App\Models\Role::class`).

- **Team ID Middleware**: Need to create or update middleware (possibly extend `EnsureActiveTenantContext` or create new middleware) that:
  - Calls `setPermissionsTeamId($tenantId)` when tenant context is set
  - Calls `setPermissionsTeamId(null)` or removes team when in system context
  - This middleware should run before permission checks

- **Permission Cache Clearing**: When tenant context changes (detected in middleware or context builder), call `app()[\Spatie\Permission\PermissionRegistrar::class]->forgetCachedPermissions()` to clear cached permissions.

- **Title Fields Migration**: Need to add migration to add title fields to both `permissions` and `roles` tables:
  - `title_ar` (string, nullable)
  - `title_en` (string, nullable)
  - Or use JSON field for translatable titles if using `spatie/laravel-translatable`

- **Tenant ID in Permissions**: Currently only `roles` table has `tenant_id`. Need to add `tenant_id` (nullable, foreign key to `tenants`) to `permissions` table for tenant-scoped permissions. Update unique constraint to include `tenant_id` where applicable.

- **Settings Pages Updates**: Update `settings/permissions` and `settings/roles` Livewire components to include:
  - Input fields for `title_ar` and `title_en` (or translatable field)
  - Validation for title fields
  - Display titles in listings instead of/in addition to names

- **Permission Model Updates**: Update `App\Models\Permission` to:
  - Add `tenant_id` to `$fillable` array
  - Add `tenant()` relationship method
  - Add title fields to `$fillable` if not using translatable package

- **Role Model Updates**: Update `App\Models\Role` to:
  - Add title fields to `$fillable` array (if not already present)

- **Seeder Verification**: Verify that seeders create the fixed roles:
  - System scope: `superadmin`
  - Tenant scope: `admin`, `teacher`, `student`
  - Ensure seeders assign proper scopes and tenant_ids where applicable

- **Unique Constraints**: Review and update unique constraints:
  - Permissions: Currently `unique(['name', 'guard_name', 'scope'])` - may need to include `tenant_id` for tenant-scoped permissions
  - Roles: Currently `unique(['tenant_id', 'name', 'guard_name'])` - verify this works correctly for system roles (where tenant_id is null)
