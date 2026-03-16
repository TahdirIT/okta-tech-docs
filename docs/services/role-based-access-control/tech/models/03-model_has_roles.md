# `model_has_roles`

## الغرض

جدول pivot يربط النماذج (Users) بالأدوار. يتم استخدام هذا الجدول لجميع الأدوار سواء على مستوى النظام أو المستأجر، مع تمييز الأدوار على مستوى المستأجر عبر عمود `tenant_id`.

> **ملاحظة مهمة:** هذا الجدول من حزمة `spatie/laravel-permission`. يتم إضافة عمود `tenant_id` لتمييز الأدوار على مستوى المستأجر.

## الأعمدة

- **role_id**: `bigint` (FK إلى `roles`)
- **model_type**: `varchar` (مثل: `App\Models\User`)
- **model_id**: `bigint` (ID النموذج)
- **team_id**: `bigint` nullable (من ميزة Teams في الحزمة - يمثل `tenant_id` عند تفعيل Teams)
- **tenant_id**: `bigint` nullable (FK إلى `tenants`) - للمستأجر المرتبط بالدور (للأدوار على مستوى المستأجر)
- **deleted_at**: `timestamptz` nullable (Soft Deletes)

## العلاقات

- **belongsTo**: `Role` (via `role_id`)
- **belongsTo**: `Tenant` (via `tenant_id`) - للأدوار على مستوى المستأجر

## الفهارس/القيود

- **primary key**: `['team_id', 'role_id', 'model_id', 'model_type']` (عند تفعيل Teams)
- أو: `['role_id', 'model_id', 'model_type']` (بدون Teams)
- **index**: (`tenant_id`) - للاستعلامات السريعة على الأدوار حسب المستأجر
- **index**: (`model_id`, `model_type`) - للاستعلامات السريعة على أدوار المستخدم
- **index**: (`deleted_at`) - للاستعلامات السريعة على السجلات المحذوفة

## القواعد

### قواعد التحقق

1. **role_id:**
   - مطلوب
   - يجب أن يكون موجوداً في جدول `roles`

2. **model_type و model_id:**
   - مطلوبان
   - يمثلان النموذج المرتبط بالدور (عادة `App\Models\User`)

3. **tenant_id:**
   - للأدوار على مستوى النظام: يجب أن يكون `null`
   - للأدوار على مستوى المستأجر: يجب أن يكون غير `null` ومطابقاً لـ `tenant_id` في جدول `roles`

### القيود

- لا يمكن ربط دور على مستوى النظام مع `tenant_id` غير `null`
- الدور على مستوى المستأجر يجب أن يكون مرتبطاً بنفس المستأجر المحدد في `tenant_id`
- عند حذف المستخدم، يتم حذف جميع الروابط تلقائياً (Cascade Delete)
- يتم استخدام Soft Deletes للحذف، مما يسمح باسترجاع الروابط المحذوفة

## الاستخدام

### ربط دور على مستوى النظام بمستخدم

```php
use App\Models\User;
use App\Models\Role;

$user = User::find($userId);
$role = Role::where('name', 'superadmin')
    ->where('scope', 'system')
    ->first();

$user->assignRole($role);
// أو
$user->roles()->attach($role->id, ['tenant_id' => null]);
```

### ربط دور على مستوى المستأجر بمستخدم

```php
use App\Models\User;
use App\Models\Role;

$user = User::find($userId);
$role = Role::where('name', 'teacher')
    ->where('scope', 'tenant')
    ->where('tenant_id', $tenantId)
    ->first();

$user->roles()->attach($role->id, ['tenant_id' => $tenantId]);
```

### الحصول على أدوار المستخدم

```php
// جميع الأدوار (غير المحذوفة)
$allRoles = $user->roles()->get();

// جميع الأدوار بما في ذلك المحذوفة
$allRolesWithTrashed = $user->roles()->withTrashed()->get();

// الأدوار على مستوى النظام فقط
$systemRoles = $user->roles()
    ->whereNull('model_has_roles.tenant_id')
    ->get();

// الأدوار على مستوى المستأجر فقط
$tenantRoles = $user->roles()
    ->whereNotNull('model_has_roles.tenant_id')
    ->where('model_has_roles.tenant_id', $tenantId)
    ->get();
```

### التحقق من وجود دور

```php
// التحقق من دور على مستوى النظام
if ($user->hasRole('superadmin')) {
    // المستخدم لديه الدور
}

// التحقق من دور على مستوى المستأجر
if ($user->roles()
    ->where('roles.name', 'teacher')
    ->where('model_has_roles.tenant_id', $tenantId)
    ->exists()) {
    // المستخدم لديه الدور في هذا المستأجر
}
```

## الفرق بين الأدوار على مستوى النظام والمستأجر

- **الأدوار على مستوى النظام**: `tenant_id` يكون `null` في `model_has_roles`
- **الأدوار على مستوى المستأجر**: `tenant_id` يحتوي على معرف المستأجر في `model_has_roles`

هذا التصميم يضمن:
- استخدام جدول واحد (`model_has_roles`) لجميع الأدوار
- العزل الكامل بين المستأجرين عبر `tenant_id`
- سهولة الاستعلام والتحقق من الأدوار
- التوافق مع حزمة `spatie/laravel-permission`

## التكامل مع spatie/laravel-permission

- يستخدم الجدول `model_has_roles` من حزمة `spatie/laravel-permission`
- يتم إضافة عمود `tenant_id` عبر Migration إضافية
- يتم إضافة عمود `deleted_at` عبر Migration إضافية لدعم Soft Deletes
- عند تفعيل Teams، يتم استخدام `team_id` أيضاً لتمثيل المستأجر
- يمكن استخدام `assignRole()` و `removeRole()` من الحزمة مع تحديد `tenant_id` عند الحاجة
- عند استخدام `removeRole()`، يتم حذف السجل بشكل ناعم (Soft Delete) ويمكن استرجاعه لاحقاً
