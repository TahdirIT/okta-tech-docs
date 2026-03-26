# `tenant_user` (Tenant ↔ User)

## الغرض

يمثل جدول الربط بين `tenants` و `users` في `okta-web`.  
في سياق `tenant-registration` يُستخدم لربط **المستخدم المالك/المدير** بالـ Tenant الجديد، ثم يمكن إسناد أدوار ضمن هذا الـ Tenant.

## الأعمدة (مطابقة لـ `okta-web`)

- **id**: `bigint` (PK)
- **tenant_id**: `bigint` (FK → `tenants.id`) `cascadeOnDelete`
- **user_id**: `bigint` (FK → `users.id`) `cascadeOnDelete`
- **created_at / updated_at**: `timestamp`
- **deleted_at**: `timestamp` (Soft Deletes)

## القيود/الفهارس (مطابقة لـ `okta-web`)

- **unique**: (`tenant_id`, `user_id`)

## العلاقات (على مستوى Eloquent)

- `TenantUser`:
  - **belongsTo**: `tenant`
  - **belongsTo**: `user`
  - **belongsToMany**: `roles` عبر جدول `tenant_user_has_roles` (مع Soft Deletes على جدول الربط)

- `Tenant`:
  - **hasMany**: `userLinks`
  - **belongsToMany**: `users` عبر `tenant_user` مع تجاهل روابط الـ pivot المحذوفة (`deleted_at`)

- `User`:
  - **hasMany**: `tenantLinks`
  - **belongsToMany**: `tenants` عبر `tenant_user` مع تجاهل روابط الـ pivot المحذوفة (`deleted_at`)

## ملاحظات

- يوجد جدولان مرتبطان بإسناد الأدوار للـ `tenant_user` في `okta-web`:  
  - `tenant_user_roles`  
  - `tenant_user_has_roles`  
  وكلاهما يحتوي `deleted_at` و `unique(tenant_user_id, role_id)`. في الموديل الحالي (`TenantUser::roles()`) يتم استخدام `tenant_user_has_roles`.

