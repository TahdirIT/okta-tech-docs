# `roles`

## الغرض

تعريف الأدوار المرجعية المستخدمة في نظام التحكم في الوصول (RBAC). الأدوار تُدار بشكل منفصل عن الصلاحيات ويمكن ربطها بعدة صلاحيات.

## النموذج

```php
App\Models\Role extends Spatie\Permission\Models\Role
```

## الجدول الأساسي (من البكج)

جدول `roles` مأخوذ مباشرة من البكج `spatie/laravel-permission`:

| الحقل | النوع | الوصف |
|------|------|-------|
| `id` | `bigint` (PK, auto increment) | المعرف الأساسي |
| `name` | `varchar(255)` | اسم الدور (مثل: `platform-admin`) |
| `guard_name` | `varchar(255)` | الحارس المستخدم (افتراضياً `web`) |
| `created_at` | `timestamp` (nullable) | تاريخ الإنشاء |
| `updated_at` | `timestamp` (nullable) | تاريخ التحديث |

**ملاحظة:** هذا الجدول مأخوذ مباشرة من البكج `spatie/laravel-permission`.

## الحقول

### الحقول الأساسية (من Spatie Package)

- **id**: `bigint` (PK, auto increment)
- **name**: `varchar(255)` (اسم الدور، مثل: `platform-admin`)
- **guard_name**: `varchar(255)` (الحارس المستخدم، افتراضياً `web`)
- **created_at / updated_at**: `timestamp` (nullable)

### الحقول الإضافية

- **tenant_id**: `bigint` nullable (FK إلى `tenants`)
  - يمكن ربط الدور بمستأجر محدد
  - `null` يعني دور عام
- **scope**: `varchar(255)` (النطاق: `tenant` أو `system`)
  - `tenant`: دور خاص بالمستأجر
  - `system`: دور على مستوى النظام
- **deleted_at**: `timestamptz` nullable (Soft Deletes)

## العلاقات

- **belongsTo**: `tenant` (optional)
- **belongsToMany**: `permissions` (via `role_has_permissions`)
- **morphToMany**: `users` (via `model_has_roles`)

## الفهارس/القيود

### من البكج الأساسي
- **unique**: (`name`, `guard_name`) - من migration `create_permission_tables.php.stub`

### من Migrations الإضافية
- **unique**: (`tenant_id`, `name`, `guard_name`) - تم تعديل unique constraint ليشمل `tenant_id`
- **foreign key**: (`tenant_id`) → `tenants.id` (cascade on delete)
- **index**: (`scope`)

## الاستخدام

### إنشاء دور

```php
use App\Models\Role;

Role::create([
    'name' => 'platform-admin',
    'guard_name' => 'web',
    'scope' => 'system',
    'tenant_id' => null,
]);
```

### البحث عن أدوار

```php
// جميع الأدوار
Role::all();

// أدوار نطاق معين
Role::where('scope', 'system')->get();

// دور مرتبط بمستأجر
Role::where('tenant_id', $tenantId)->get();

// دور محدد
Role::where('name', 'platform-admin')->first();
```

### ربط صلاحيات بدور

```php
$role->givePermissionTo('manage-users');
$role->syncPermissions(['manage-users', 'view-reports']);

// أو عبر العلاقة
$role->permissions()->attach($permissionId);
$role->permissions()->sync([$permissionId1, $permissionId2]);
```

### تعيين دور لمستخدم

```php
$user->assignRole('platform-admin');
$user->syncRoles(['admin', 'manager']);
$user->removeRole('guest');
```

### التحقق من الدور

```php
$user->hasRole('platform-admin');
$user->hasAnyRole(['admin', 'manager']);
```

## المقارنة مع البكج الأساسي

النموذج المخصص `App\Models\Role` يمتد من `Spatie\Permission\Models\Role` ويضيف الحقول التالية:

### الحقول الإضافية المضافة

| الحقل | النوع | الوصف |
|------|------|-------|
| `tenant_id` | `bigint` nullable | FK إلى `tenants` |
| `scope` | `varchar(255)` | النطاق: `tenant` أو `system` |
| `deleted_at` | `timestamptz` nullable | Soft Deletes |

### جدول المقارنة

| الميزة | البكج الأساسي | النموذج المخصص |
|--------|---------------|----------------|
| الحقول الأساسية | `id`, `name`, `guard_name`, `created_at`, `updated_at` | نفس الحقول + `tenant_id`, `scope`, `deleted_at` |
| العلاقات | `belongsToMany: permissions`, `morphToMany: users` | نفس العلاقات + `belongsTo: tenant` |
| الفهارس | `unique: (name, guard_name)` | `unique: (tenant_id, name, guard_name)` |
| Soft Deletes | غير مدعوم | مدعوم |
| Multi-tenancy | غير مدعوم | مدعوم عبر `tenant_id` |

## ملاحظات

- الأدوار تُستخدم كمرجع في النظام
- يمكن اكتشاف الأدوار المستخدمة في الكود عبر `RbacDiscoveryService`
- الأدوار على مستوى النظام (`system`) متاحة لجميع المستأجرين
- الأدوار على مستوى المستأجر (`tenant`) خاصة بكل مستأجر
- يمكن ربط دور بعدة صلاحيات، مما يوفر مرونة في تنظيم الوصول
- الجدول الأساسي مأخوذ من البكج `spatie/laravel-permission`