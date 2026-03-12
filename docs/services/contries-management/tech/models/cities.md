# `cities`

## الغرض

تعريف المدن التابعة لمنطقة.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **region_id**: `bigint` (FK → `regions.id`)
- **name_ar**: `varchar` nullable
- **name_en**: `varchar` nullable
- **name_json**: `jsonb` nullable
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **belongsTo**: `regions`
- **hasMany**: `districts`

## الفهارس/القيود

- **index**: (`region_id`)

## مقارنة مع `v5website`

موجود ومطابق تقريباً (مع اقتراح `jsonb` بدلاً من `json`).

