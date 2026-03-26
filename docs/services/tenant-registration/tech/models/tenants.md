# `tenants`

## الغرض

تمثيل الكيان (Tenant) الذي يتم إنشاؤه عبر خدمة تسجيل الكيان، وربطه بالدولة ونوع الكيان وبعض البيانات المرجعية المطلوبة للتفعيل والحوكمة.

## أعمدة مقترحة (مستقلة عن الـ ORM)

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique (للـ APIs العامة)
- **country_id**: `bigint` (FK → `countries.id`)
- **tenant_type**: `varchar` (مثل: `administrative_school`, `individual_teacher`, …)
- **name**: `varchar`
- **education_level_group_id**: `bigint` nullable (FK → `education_level_groups.id`)
  - مطلوب عندما يكون `tenant_type` = **مدرسة إدارية** أو **معلم فردي**
- **custom_fields**: `jsonb` nullable (key/value بعد التحقق)
- **activation_status**: `varchar` default `pending_verification` (مثل: `pending_verification | active | blocked`)
- **created_by_user_id**: `bigint` nullable (FK → `users.id`) — المستخدم المالك
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **belongsTo**: `countries`
- **belongsTo (nullable)**: `education_level_groups` (من خدمة/مفهوم إدارة الدول)
- **belongsTo**: `users` (Owner account) عبر `created_by_user_id`

## القيود/الفهارس المقترحة

- **unique**: (`ulid`)
- **index**: (`country_id`)
- **index**: (`tenant_type`)
- (اختياري) **unique**: (`country_id`, `name`) إن كانت السياسة تمنع تكرار الاسم داخل الدولة

## ملاحظات

- مصدر تعريف `education_level_groups` موثق في:
  - `docs/services/contries-management/guide/stages-management.md`
  - `docs/services/contries-management/tech/models/education_level_groups.md`

