# `districts`

## الغرض

تعريف الأحياء التابعة لمدينة (وممكن ربطها مباشرة بالمنطقة أيضاً حسب البيانات المستوردة).

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **city_id**: `bigint` (FK → `cities.id`)
- **region_id**: `bigint` (FK → `regions.id`)
- **name_ar**: `varchar` nullable
- **name_en**: `varchar` nullable
- **name_json**: `jsonb` nullable
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **belongsTo**: `cities`
- **belongsTo**: `regions`

## الفهارس/القيود

- **index**: (`city_id`)
- **index**: (`region_id`)

## مقارنة مع `v5website`

موجود ومطابق تقريباً (مع اقتراح `jsonb` بدلاً من `json`).

