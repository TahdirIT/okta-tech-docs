# `tenant_login_methods`

## الغرض

تعريف طرق تسجيل الدخول المسموحة لكل Tenant في `okta-web`، مع إمكانية تفعيل/تعطيل كل طريقة.

## الأعمدة (مطابقة لـ `okta-web`)

- **id**: `bigint` (PK)
- **tenant_id**: `bigint` (FK → `tenants.id`) `cascadeOnDelete`
- **method**: `varchar`
  - قيم شائعة (حسب تعليق migration في `okta-web`): `password | national_id | nafath | microsoft`
- **enabled**: `boolean` default `true`
- **created_at / updated_at**: `timestamp`
- **deleted_at**: `timestamp` (Soft Deletes)

## القيود/الفهارس (مطابقة لـ `okta-web`)

- **unique**: (`tenant_id`, `method`)

## العلاقات (على مستوى Eloquent)

- `TenantLoginMethod`:
  - **belongsTo**: `tenant`

- `Tenant`:
  - **hasMany**: `loginMethods` (مفعّلة فقط + غير محذوفة)

