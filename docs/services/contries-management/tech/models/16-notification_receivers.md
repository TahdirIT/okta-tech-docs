# `notification_receivers` (خارج نطاق إدارة الدول، لكن مرتبط بنظام الإشعارات)

## الغرض

تخزين المستلمين لكل إشعار (receiver polymorphic) وحالة الإرسال لكل قناة.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique (ULID للاستخدام في APIs العامة)
- **notification_id**: `bigint` (FK → `notifications.id`)
- **receiver_type / receiver_id**: morphs
- **type**: `varchar` nullable
- **app / sms / watsi**: `boolean` defaults
- **status**: `varchar` default `pending`
- **note**: `varchar` nullable
- **data**: `jsonb` nullable
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## الفهارس/القيود (مقترح)

- **unique**: (`ulid`)
- **index**: (`notification_id`)
- **index**: (`receiver_type`, `receiver_id`)
- **index**: (`status`)


