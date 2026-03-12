# `countries`

## الغرض

تعريف الدول كمرجع أساسي تُبنى عليه إعدادات الدولة وبقية البيانات التابعة لها.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique (ULID للاستخدام في APIs العامة)
- **name_ar**: `varchar` nullable
- **name_en**: `varchar` nullable
- **name_json**: `jsonb` nullable (للدعم متعدد اللغات عند الحاجة)
- **code**: `varchar` nullable (مثل: SA, KW)
- **phone_code**: `varchar` nullable
- **flag**: `varchar` nullable
- **timezone**: `varchar` nullable (مثل: `Asia/Riyadh`)
- **active**: `boolean` default `true`
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **hasMany**: `regions`
- **hasMany**: `academic_years`
- **hasMany**: `education_level_groups`
- (اختياري) **hasMany**: `education_levels`
- (اختياري) **hasMany**: `subjects`
- **morphMany**: `holiday_schedules` (via `related_type/related_id`)
- **morphOne**: `model_settings` (via `model_type/model_id`)

## الفهارس/القيود

- **unique**: (`code`) إن كانت مطلوبة كقيمة فريدة
- **unique**: (`ulid`)
- **index**: (`active`)


