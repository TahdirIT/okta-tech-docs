# `holiday_schedules`

## الغرض

جدول الإجازات والأنشطة على مستوى الدولة/المدرسة.

## الأعمدة (مقترح Laravel 12 + PostgreSQL)

- **id**: `bigint` (PK)
- **title**: `jsonb` (يدعم العربية/الإنجليزية)
- **related_type**: `varchar` (polymorphic: `App\\Models\\Country` أو `App\\Models\\School`)
- **related_id**: `bigint`
- **type**: `varchar` (مثل: `HOLIDAY`, `ACTIVITY`)
- **start_at**: `date`
- **end_at**: `date`
- **register_absent**: `boolean` default `false`
- **send_notifications**: `boolean` default `true`
- **notified_users**: `jsonb` nullable (قائمة المستفيدين/roles)
- **send_notifications_at**: `timestamptz` nullable
- **notification_content**: `text` nullable (كما في الدليل)
- **deleted_at**: `timestamptz` nullable
- **created_at / updated_at**: `timestamptz`

## العلاقات

- **morphTo**: `related`

## الفهارس/القيود

- **index**: (`related_type`, `related_id`)
- **index**: (`start_at`, `end_at`)
- (مقترح) **check**: `end_at >= start_at`
- (مقترح Postgres) منع تداخل الإجازات ضمن نفس النطاق يمكن تنفيذه عبر:
  - منطق تطبيق + استعلامات overlap
  - أو `EXCLUDE USING gist` على `daterange(start_at,end_at,'[]')` مع `related_*` (يتطلب تصميم إضافي)

## مقارنة مع `v5website`

موجود، لكن في `v5website` لا يظهر عمود `notification_content` في migration الأساسي (تمت إضافته لاحقاً). هنا نوثّقه كحقل أساسي لأنه مذكور في الدليل.

