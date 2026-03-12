# `cities`

## الغرض

تعريف المدن التابعة لمنطقة.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique (ULID للاستخدام في APIs العامة)
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

- **unique**: (`ulid`)
- **index**: (`region_id`)


