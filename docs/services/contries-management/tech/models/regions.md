# `regions`

## الغرض

تعريف المناطق التابعة لدولة (Regions) ضمن الهيكل الجغرافي.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **country_id**: `bigint` (FK → `countries.id`)
- **capital_city_id**: `bigint` nullable (مرجع منطقي لمدينة العاصمة إن لزم)
- **name_ar**: `varchar` nullable
- **name_en**: `varchar` nullable
- **name_json**: `jsonb` nullable
- **code**: `varchar` nullable
- **national_id**: `varchar` nullable (كما يظهر في الدليل)
- **center**: `varchar` nullable (إحداثيات نصية أو WKT إن لزم)
- **boundaries**: `geometry` nullable (يتطلب PostGIS)
- **population**: `bigint` nullable
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **belongsTo**: `countries`
- **hasMany**: `cities`
- **hasMany**: `districts` (إن كان الأحياء مرتبطة أيضاً بالمنطقة)

## الفهارس/القيود

- **index**: (`country_id`)
- (اختياري) **unique**: (`country_id`, `code`)

## مقارنة مع `v5website`

موجود: `country_id`, `capital_city_id`, `code`, `center`, `boundaries`, `population` + حقول الاسم والترجمة.
الزيادة المقترحة: `national_id`.

