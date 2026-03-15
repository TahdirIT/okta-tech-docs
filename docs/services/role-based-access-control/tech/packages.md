# البكجات المستخدمة - إدارة الصلاحيات والأدوار

## نظرة عامة

يستخدم نظام إدارة الصلاحيات والأدوار البكج `spatie/laravel-permission` كأساس رئيسي لإدارة الصلاحيات والأدوار في قاعدة البيانات. هذا البكج يوفر البنية الأساسية والجداول والعلاقات اللازمة لنظام RBAC (Role-Based Access Control).

## البكج الأساسي: `spatie/laravel-permission`

### الوصف

`spatie/laravel-permission` هو بكج Laravel لإدارة الأدوار والصلاحيات في قاعدة البيانات. يتكامل مع Laravel Gates ويدعم:
- الصلاحيات المباشرة
- الأدوار
- عدة حراس (Multiple Guards)
- Blade Directives
- فحوصات التفويض

### Migrations البكج

البكج `spatie/laravel-permission` يحتوي على ملفين migrations فقط:

1. **`create_permission_tables.php.stub`**: ينشئ الجداول الأساسية:
   - `permissions`: جدول الصلاحيات
   - `roles`: جدول الأدوار
   - `model_has_permissions`: ربط الصلاحيات بالمستخدمين (Polymorphic)
   - `model_has_roles`: ربط الأدوار بالمستخدمين (Polymorphic)
   - `role_has_permissions`: ربط الصلاحيات بالأدوار

2. **`add_teams_fields.php.stub`**: يضيف حقول teams (اختياري، يعمل فقط إذا كان `config('permission.teams')` مفعّل)

### الجداول الوسيطة (Pivot Tables)

يوفر البكج الجداول الوسيطة التالية:
- `model_has_permissions`: ربط الصلاحيات بالمستخدمين (Polymorphic)
- `model_has_roles`: ربط الأدوار بالمستخدمين (Polymorphic)
- `role_has_permissions`: ربط الصلاحيات بالأدوار

**ملاحظة:** لمزيد من التفاصيل حول جداول `permissions` و `roles` والنماذج المخصصة، راجع ملفات `models/01-permissions.md` و `models/02-roles.md`.

## الاستخدام في النظام

### المزايا الرئيسية للبكج

1. **التكامل مع Laravel Gates**: يمكن استخدام `$user->can('permission-name')` مباشرة
2. **Blade Directives**: دعم `@can`, `@cannot`, `@role`, `@hasrole` في القوالب
3. **Caching**: تخزين مؤقت تلقائي للأدوار والصلاحيات لتحسين الأداء
4. **Multiple Guards**: دعم عدة حراس (web, api, etc.)
5. **Polymorphic Relations**: ربط مرن بالعديد من النماذج

### التوسعات المضافة

1. **Multi-tenancy**: إضافة دعم المستأجرين عبر `tenant_id`
2. **Scope Management**: إدارة النطاقات (`tenant` vs `system`)
3. **Soft Deletes**: إمكانية استرجاع البيانات المحذوفة
4. **Custom Indexes**: فهارس مخصصة لتحسين الأداء

## أمثلة الاستخدام

### استخدام البكج الأساسي

```php
use Spatie\Permission\Models\Permission;
use Spatie\Permission\Models\Role;

// إنشاء صلاحية
$permission = Permission::create(['name' => 'edit articles']);

// إنشاء دور
$role = Role::create(['name' => 'writer']);

// ربط صلاحية بدور
$role->givePermissionTo($permission);

// تعيين دور لمستخدم
$user->assignRole('writer');

// التحقق من الصلاحية
$user->can('edit articles');
```

## ملاحظات مهمة

1. **الجداول الأساسية**: الجداول `permissions` و `roles` مأخوذة مباشرة من البكج `spatie/laravel-permission` (راجع `models/01-permissions.md` و `models/02-roles.md` للتفاصيل)
2. **التوسعات**: الحقول الإضافية (`scope`, `tenant_id`, `deleted_at`) تُضاف عبر migrations منفصلة
3. **التوافق**: جميع الوظائف الأساسية للبكج تعمل مع النماذج المخصصة
4. **الترقية**: عند ترقية البكج، يجب التأكد من توافق التوسعات المضافة
