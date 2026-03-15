# `permissions`

## الغرض

تعريف الصلاحيات المرجعية المستخدمة في نظام التحكم في الوصول (RBAC). الصلاحيات تُدار بشكل منفصل عن الأدوار ويمكن ربطها بعدة أدوار.

## النموذج

```php
App\Models\Permission extends Spatie\Permission\Models\Permission
```

## الجدول الأساسي (من البكج)

جدول `permissions` مأخوذ مباشرة من البكج `spatie/laravel-permission`:

| الحقل | النوع | الوصف |
|------|------|-------|
| `id` | `bigint` (PK, auto increment) | المعرف الأساسي |
| `name` | `varchar(255)` | اسم الصلاحية (مثل: `manage-users`) |
| `guard_name` | `varchar(255)` | الحارس المستخدم (افتراضياً `web`) |
| `created_at` | `timestamp` (nullable) | تاريخ الإنشاء |
| `updated_at` | `timestamp` (nullable) | تاريخ التحديث |

**ملاحظة:** هذا الجدول مأخوذ مباشرة من البكج `spatie/laravel-permission`.

## الحقول

### الحقول الأساسية (من Spatie Package)

- **id**: `bigint` (PK, auto increment)
- **name**: `varchar(255)` (اسم الصلاحية، مثل: `manage-users`)
- **guard_name**: `varchar(255)` (الحارس المستخدم، افتراضياً `web`)
- **created_at / updated_at**: `timestamp` (nullable)

### الحقول الإضافية

- **scope**: `varchar(255)` (النطاق: `tenant` أو `system`)
  - `tenant`: صلاحية خاصة بالمستأجر
  - `system`: صلاحية على مستوى النظام
- **deleted_at**: `timestamptz` nullable (Soft Deletes)

## العلاقات

- **belongsToMany**: `roles` (via `role_has_permissions`)
- **morphToMany**: `users` (via `model_has_permissions`)

## الفهارس/القيود

### من البكج الأساسي
- **unique**: (`name`, `guard_name`) - من migration `create_permission_tables.php.stub`

### من Migrations الإضافية
- **unique**: (`name`, `guard_name`, `scope`) - تم تعديل unique constraint ليشمل `scope`
- **index**: (`scope`)

## الاستخدام

### إنشاء صلاحية

```php
use App\Models\Permission;

Permission::create([
    'name' => 'manage-users',
    'guard_name' => 'web',
    'scope' => 'tenant',
]);
```

### البحث عن صلاحيات

```php
// جميع الصلاحيات
Permission::all();

// صلاحيات نطاق معين
Permission::where('scope', 'system')->get();

// صلاحية محددة
Permission::where('name', 'manage-users')->first();
```

### ربط صلاحية بدور

```php
$role->givePermissionTo('manage-users');
$role->syncPermissions(['manage-users', 'view-reports']);
```

### التحقق من الصلاحية

```php
$user->hasPermissionTo('manage-users');
$user->can('manage-users');
```

## المقارنة مع البكج الأساسي

النموذج المخصص `App\Models\Permission` يمتد من `Spatie\Permission\Models\Permission` ويضيف الحقول التالية:

### الحقول الإضافية المضافة

| الحقل | النوع | الوصف |
|------|------|-------|
| `scope` | `varchar(255)` | النطاق: `tenant` أو `system` |
| `deleted_at` | `timestamptz` nullable | Soft Deletes |

### جدول المقارنة

| الميزة | البكج الأساسي | النموذج المخصص |
|--------|---------------|----------------|
| الحقول الأساسية | `id`, `name`, `guard_name`, `created_at`, `updated_at` | نفس الحقول + `scope`, `deleted_at` |
| العلاقات | `belongsToMany: roles`, `morphToMany: users` | نفس العلاقات |
| الفهارس | `unique: (name, guard_name)` | `unique: (name, guard_name, scope)` |
| Soft Deletes | غير مدعوم | مدعوم |

## ملاحظات

- الصلاحيات تُستخدم كمرجع في النظام
- يمكن اكتشاف الصلاحيات المستخدمة في الكود عبر `RbacDiscoveryService`
- الصلاحيات على مستوى النظام (`system`) متاحة لجميع المستأجرين
- الصلاحيات على مستوى المستأجر (`tenant`) خاصة بكل مستأجر
- الجدول الأساسي مأخوذ من البكج `spatie/laravel-permission`