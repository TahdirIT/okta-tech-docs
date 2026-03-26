# `tenants`

## الغرض

تمثيل الكيان (Tenant) في مشروع `okta-web`، وهو الكيان الذي يتم:

- ربط المستخدمين به (عبر `tenant_user`)
- إعداد طرق تسجيل الدخول الخاصة به (عبر `tenant_login_methods`)

## الأعمدة (مطابقة لـ `okta-web`)

- **id**: `bigint` (PK)
- **name**: `varchar`
- **type**: `varchar`
  - قيم شائعة (حسب تعليق migration في `okta-web`): `school | kindergarten | institute | academy | college | university`
- **country_id**: `bigint` nullable (FK → `countries.id`)
- **status**: `varchar` default `active`
  - قيم شائعة (حسب تعليق migration في `okta-web`): `active | suspended`
- **created_at / updated_at**: `timestamp`
- **deleted_at**: `timestamp` (Soft Deletes)

## العلاقات

- **belongsTo**: `country` (→ `countries`)
- **hasMany**: `userLinks` (→ `tenant_user` rows via `TenantUser`)
- **belongsToMany**: `users` عبر pivot جدول `tenant_user` (مع `deleted_at` على الـ pivot)
- **hasMany**: `loginMethods` (→ `tenant_login_methods`) مع فلترة `enabled=true` و `deleted_at is null`

## القيود/الفهارس (مطابقة لـ `okta-web`)

- لا توجد قيود unique أو فهارس إضافية معرفة في migration لجدول `tenants` (عدا القيود الافتراضية للمفاتيح الأجنبية).
- **FK**: `country_id` يقبل `null` ويتم `nullOnDelete()` عند حذف الدولة.

## ملاحظات

- التوثيق السابق كان يفترض حقولًا مثل `ulid`, `tenant_type`, `education_level_group_id`, `custom_fields`, `created_by_user_id` و `activation_status` — هذه **غير موجودة حاليًا** في `okta-web`.
- إذا كانت خدمة `tenant-registration` تحتاج Wizard وحقولًا ديناميكية حسب الدولة/النوع، فهذه إضافات مستقبلية يمكن تنفيذها، راجع `tenant_registration_sessions.md` كاقتراح.

