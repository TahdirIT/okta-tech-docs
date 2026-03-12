# `notifications` (خارج نطاق إدارة الدول، لكن مرتبط بنظام الإشعارات)

## الغرض

تخزين الإشعارات المرسلة/المنشأة فعلياً (سجل الإرسال)، بينما `notification_definitions` يمثل القوالب/التعريفات.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique (ULID للاستخدام في APIs العامة)
- **sender_type / sender_id**: nullable morphs
- **title**: `varchar`
- **content**: `text`
- **file**: `varchar` nullable
- **type**: `varchar`
- **app / sms / watsi**: `boolean` defaults
- **status**: `varchar` default `pending`
- **note**: `varchar` nullable
- **causer_type / causer_id**: nullable morphs
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## الفهارس/القيود (مقترح)

- **unique**: (`ulid`)
- **index**: (`status`)
- **index**: (`created_at`)
- **index**: (`sender_type`, `sender_id`)


