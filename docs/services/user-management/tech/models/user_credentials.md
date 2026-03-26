# `user_credentials`

## الغرض

تخزين بيانات الاعتماد (Credentials) للمستخدم بشكل منفصل عن جدول `users`.

في `okta-web` يتم استخدام سجل واحد لكل مستخدم (1:1) ويتم ربطه عبر `user_id` كمفتاح أساسي.

## أعمدة موجودة في المشروع (`okta-web`)

- **user_id**: `bigint` (PK, FK -> `users.id`, cascade on delete)
- **password_hash**: `varchar`
- **last_changed_at**: `timestamp` nullable
- **created_at / updated_at**: timestamps

