# `tenant_registration_sessions` (اختياري)

## الغرض

دعم تجربة Wizard متعددة الخطوات مع حفظ مؤقت/قابل للاستئناف (Draft) خصوصًا عندما:

- تكون الحقول ديناميكية حسب الدولة والنوع
- توجد خطوات تحقق/توثيق لاحقة
- نحتاج ربط “محاولة التسجيل” بالأحداث (Events) والتتبع (Analytics)

## أعمدة مقترحة

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique
- **country_id**: `bigint` nullable
- **tenant_type**: `varchar` nullable
- **education_level_group_id**: `bigint` nullable
- **draft_payload**: `jsonb` (مدخلات wizard بدون كلمة المرور/بيانات حساسة)
- **status**: `varchar` default `draft` (مثل: `draft | submitted | created | cancelled`)
- **owner_user_id**: `bigint` nullable (FK → `users.id`) — عند “لدي حساب” أو بعد إنشاء المستخدم
- **tenant_id**: `bigint` nullable (FK → `tenants.id`) — بعد الإنشاء
- **created_at / updated_at**: `timestamptz`

## ملاحظات

- يجب عدم تخزين كلمة المرور أو OTP أو أسرار حساسة داخل `draft_payload`.

