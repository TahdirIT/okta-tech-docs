# `users` (Owner account)

## الغرض

المستخدم المالك (Owner/Admin) الذي يتم:

- إنشاؤه ضمن تدفق تسجيل الكيان، أو
- ربطه بكيان جديد إذا كان لديه حساب مسبق.

## أعمدة أساسية مقترحة

- **id**: `bigint` (PK)
- **ulid**: `char(26)` unique
- **username**: `varchar` unique
- **name**: `varchar`
- **national_id**: `varchar` nullable (وقد يكون إلزاميًا حسب الدولة)
- **mobile**: `varchar` nullable
- **email**: `varchar` nullable
- **mobile_verified**: `boolean` default `false`
- **email_verified**: `boolean` default `false`
- **password_hash**: `varchar`
- **created_at / updated_at**: `timestamptz`

## منع التكرار (Uniqueness checks)

عند إنشاء حساب جديد يجب منع التسجيل المكرر لهذه الحقول:

- **national_id**
- **username**
- **mobile**
- **email**

> في حال وجود حساب مسبق، يجب توجيه المستخدم لمسار “لدي حساب” بدل إنشاء حساب جديد بنفس البيانات.

## ملاحظات مرتبطة بالتفعيل

- حالة “مفعّل/غير مفعّل” في سياق التسجيل تعتمد على:
  - `mobile_verified`
  - `email_verified`
  - وإلزامية كل قناة حسب إعدادات الدولة في:
    - `docs/services/contries-management/guide/entity-registration-customizations.md`

