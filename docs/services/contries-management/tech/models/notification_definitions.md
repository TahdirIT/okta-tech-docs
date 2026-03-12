# `notification_definitions`

## الغرض

تعريف محتوى الإشعارات وقنواتها على مستوى الدولة، مع دعم تخصيص (override) على مستوى المدرسة عند الحاجة.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **country_id**: `bigint` nullable (FK → `countries.id`, `nullOnDelete`)
- **school_id**: `bigint` nullable (FK → `schools.id`, `nullOnDelete`) — خارج نطاق خدمة إدارة الدول لكن مستخدم للـ override
- **slug**: `varchar` (صيغة: `groupSlug.definitionSlug`)
- **group_name**: `jsonb`
- **title**: `jsonb`
- **content**: `text` nullable
- **variables**: `jsonb` nullable (كما في الدليل)
- **app_status / sms_status / watsi_status**: `varchar` nullable (مثل: `forced|active|inactive`) (مقترح)
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## الفهارس/القيود

- **unique**: (`country_id`, `school_id`, `slug`)
- **index**: (`country_id`)
- **index**: (`school_id`)

## مقارنة مع `v5website`

موجود: (`country_id`, `school_id`, `slug`, `group_name`, `title`, `content`) مع unique مركّب.
الزيادة المقترحة: `variables` وحالات القنوات بشكل صريح (لأن الدليل يذكر forced/active/inactive).

