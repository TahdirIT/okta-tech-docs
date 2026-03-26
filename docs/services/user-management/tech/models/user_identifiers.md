# `user_identifiers`

## الغرض

تخزين "معرفات" المستخدم (Login identifiers) وقنوات التواصل، بدل تخزينها مباشرةً في جدول `users`.

هذا التصميم يسمح بدعم عدة أنواع معرفات للمستخدم (username/email/phone/national_id/SSO) مع خصائص مثل التحقق و"المعرف الأساسي".

## أعمدة موجودة في المشروع (`okta-web`)

- **id**: `bigint` (PK)
- **user_id**: `bigint` (FK -> `users.id`, cascade on delete)
- **type**: `varchar`
  - قيم مستخدمة/مذكورة في المشروع: `username | email | phone | national_id | sso_nafath | sso_microsoft`
- **value**: `varchar`
- **country_id**: `bigint` nullable (FK -> `countries.id`, null on delete)
- **verified_at**: `timestamp` nullable
- **is_primary**: `boolean` default `false`
- **created_at / updated_at**: timestamps
- **deleted_at**: soft deletes

## الفهارس ومنع التكرار (Uniqueness)

يوجد قيد فريد في المشروع:

- `unique(type, value, country_id)`

> ملاحظة: وجود `country_id` ضمن المفتاح الفريد يعني أن بعض المعرفات قد تكون "محلية" حسب الدولة (مثل رقم الهوية الوطنية)، بينما قد تُترك `country_id = null` لمعرفات عالمية حسب سياسة المنتج.

## علاقة التحقق (Verification)

بدلاً من `mobile_verified/email_verified` في جدول `users`، يتم استخدام:

- `verified_at != null` كمؤشر تحقق لهذا المعرف (email/phone…).

