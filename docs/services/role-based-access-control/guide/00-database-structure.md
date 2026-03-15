# Database structure (Laravel 12 + PostgreSQL)

هذا القسم يوضح **هيكل قاعدة البيانات** لخدمة **إدارة الصلاحيات والأدوار** مع افتراض:

- **Laravel 12**
- **PostgreSQL**
- **Spatie Laravel Permission Package**

> الهدف: توفير نظام مرجعي للصلاحيات والأدوار مع إمكانية اكتشاف الصلاحيات والأدوار المستخدمة في الكود واستيرادها تلقائياً.

## الجداول الأساسية

### 1) `permissions`

جدول الصلاحيات المرجعية.

**الأعمدة الأساسية:**
- **id**: `bigint` (PK)
- **name**: `varchar` (اسم الصلاحية، مثل: `manage-users`)
- **guard_name**: `varchar` (الحارس المستخدم، مثل: `web`)
- **scope**: `varchar` (النطاق: `tenant` أو `system`)
- **deleted_at**: `timestamptz` nullable (Soft Deletes)
- **created_at / updated_at**: `timestamptz`

**الفهارس/القيود:**
- **unique**: (`name`, `guard_name`, `scope`)

### 2) `roles`

جدول الأدوار المرجعية.

**الأعمدة الأساسية:**
- **id**: `bigint` (PK)
- **tenant_id**: `bigint` nullable (FK إلى `tenants`)
- **name**: `varchar` (اسم الدور، مثل: `platform-admin`)
- **guard_name**: `varchar` (الحارس المستخدم، مثل: `web`)
- **scope**: `varchar` (النطاق: `tenant` أو `system`)
- **deleted_at**: `timestamptz` nullable (Soft Deletes)
- **created_at / updated_at**: `timestamptz`

**الفهارس/القيود:**
- **unique**: (`tenant_id`, `name`, `guard_name`)
- **foreign key**: (`tenant_id`) → `tenants.id` (cascade on delete)

### 3) `role_has_permissions`

جدول الربط بين الأدوار والصلاحيات (Pivot Table).

**الأعمدة:**
- **permission_id**: `bigint` (FK إلى `permissions.id`)
- **role_id**: `bigint` (FK إلى `roles.id`)

**الفهارس/القيود:**
- **primary key**: (`permission_id`, `role_id`)
- **foreign key**: (`permission_id`) → `permissions.id` (cascade on delete)
- **foreign key**: (`role_id`) → `roles.id` (cascade on delete)

### 4) `model_has_permissions`

جدول ربط الصلاحيات مباشرة بالنماذج (Polymorphic).

**الأعمدة:**
- **permission_id**: `bigint` (FK إلى `permissions.id`)
- **model_type**: `varchar` (نوع النموذج، مثل: `App\Models\User`)
- **model_id**: `bigint` (معرف النموذج)

**الفهارس/القيود:**
- **primary key**: (`permission_id`, `model_id`, `model_type`)
- **foreign key**: (`permission_id`) → `permissions.id` (cascade on delete)
- **index**: (`model_id`, `model_type`)

### 5) `model_has_roles`

جدول ربط الأدوار مباشرة بالنماذج (Polymorphic).

**الأعمدة:**
- **role_id**: `bigint` (FK إلى `roles.id`)
- **model_type**: `varchar` (نوع النموذج، مثل: `App\Models\User`)
- **model_id**: `bigint` (معرف النموذج)

**الفهارس/القيود:**
- **primary key**: (`role_id`, `model_id`, `model_type`)
- **foreign key**: (`role_id`) → `roles.id` (cascade on delete)
- **index**: (`model_id`, `model_type`)

## العلاقات

### Permission Model
- **belongsToMany**: `roles` (via `role_has_permissions`)
- **morphToMany**: `users` (via `model_has_permissions`)

### Role Model
- **belongsTo**: `tenant` (optional)
- **belongsToMany**: `permissions` (via `role_has_permissions`)
- **morphToMany**: `users` (via `model_has_roles`)

## ملاحظات مهمة

- يتم استخدام حزمة **Spatie Laravel Permission** كأساس للنظام
- الصلاحيات والأدوار منفصلة تماماً ويمكن إدارتها بشكل مستقل
- النطاق (`scope`) يحدد ما إذا كانت الصلاحية أو الدور على مستوى المستأجر (`tenant`) أو النظام (`system`)
- يتم اكتشاف الصلاحيات والأدوار المستخدمة في الكود عبر `RbacDiscoveryService` وتخزين التقرير في `storage/app/rbac/missing-rbac.json`
