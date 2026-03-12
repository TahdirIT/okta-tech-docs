# `notification_receivers` (خارج نطاق إدارة الدول، لكن مرتبط بنظام الإشعارات)

## الغرض

تخزين المستلمين لكل إشعار (receiver polymorphic) وحالة الإرسال لكل قناة.

## الأعمدة (كما في `v5website` - قابلة للتحسين على Postgres)

- **id**: `bigint` (PK)
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

- **index**: (`notification_id`)
- **index**: (`receiver_type`, `receiver_id`)
- **index**: (`status`)

## مقارنة مع `v5website`

مطابق (مع اقتراح `jsonb` بدل `json` لـ `data`).

