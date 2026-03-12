# `model_settings`

## الغرض

تخزين إعدادات مرنة (key/value) مرتبطة بأي Model (polymorphic).

في سياق **إدارة الدول** تُستخدم عادةً لتخزين:

- **`weekdays`**: إعدادات أيام الأسبوع على مستوى الدولة
- **`active_term_id`**: الفصل النشط

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **model_type**: `varchar`
- **model_id**: `bigint`
- **settings**: `jsonb`
- **created_at / updated_at**: `timestamptz`

## الفهارس/القيود

- **unique**: (`model_type`, `model_id`)
- (اختياري) **GIN index** على `settings` لدعم queries على `settings->...`

## مقارنة مع `v5website`

موجود بنفس الفكرة، مع أمثلة فعلية على:

- `weekdays` كقائمة أيام مع `is_active`
- `active_term_id` كقيمة نصية داخل JSON

