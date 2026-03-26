# الأحداث (Event triggers) - Tenant Registration

هذا المستند يُعرّف الأحداث التي تُطلق أثناء تسجيل Tenant جديد والتحقق منه، بهدف دعم التكامل بنمط **Event-Driven** مع خدمات مستقبلية (Notifications, Provisioning, Analytics, Onboarding, …).

> ملاحظة: أسماء الأحداث وبنيتها قابلة للتحديث، لكن يُفضل اعتماد نمط ثابت للأسماء والإصدارات.

## مبادئ عامة

- **الاسم**: بصيغة `tenant_registration.<event_name>.v1`
- **المعرفات**: يجب تضمين `tenant_id` و`user_id` عند توفرهما.
- **الخصوصية**: لا ترسل كلمة المرور أو رموز OTP أو بيانات حساسة غير ضرورية.
- **النسخ (Versioning)**: عند تغيير payload بطريقة كاسرة يتم إصدار `v2`.

## 1) tenant_registration.submitted.v1

يُطلق عند استلام طلب التسجيل (بعد التحقق المبدئي من صحة المدخلات وقبل/أو بعد الإنشاء حسب قرار التنفيذ).

Payload مقترح:

- **country_id**
- **tenant_type**
- **tenant_name**
- **custom_fields** (قائمة key/value بعد التحقق)
- **owner**: `{ username, name, national_id, mobile, email }` (مع مراعاة إخفاء ما يلزم)

## 2) tenant_registration.created.v1

يُطلق بعد إنشاء Tenant + المستخدم المالك بنجاح.

Payload مقترح:

- **tenant_id**
- **country_id**
- **tenant_type**
- **tenant_name**
- **owner_user_id**
- **contact_requirements**: `{ username_required, national_id_required, mobile_required, email_required }`
- **activation_status**: `pending_verification`

## 3) tenant_registration.verification.mobile_started.v1

يُطلق عند بدء/إعادة إرسال عملية التحقق من الجوال (OTP).

Payload مقترح:

- **tenant_id**
- **user_id**
- **mobile** (قد يكون مُقنع Masked)
- **attempt** (رقم المحاولة أو timestamp)

## 4) tenant_registration.verification.email_started.v1

يُطلق عند بدء/إعادة إرسال عملية التحقق من البريد (رابط/رمز).

Payload مقترح:

- **tenant_id**
- **user_id**
- **email** (قد يكون مُقنع Masked)
- **attempt**

## 5) tenant_registration.verified.mobile.v1

يُطلق عند نجاح تحقق الجوال.

Payload مقترح:

- **tenant_id**
- **user_id**
- **verified_at**

## 6) tenant_registration.verified.email.v1

يُطلق عند نجاح تحقق البريد.

Payload مقترح:

- **tenant_id**
- **user_id**
- **verified_at**

## 7) tenant_registration.activated.v1

يُطلق عندما يصبح الحساب/الكيان “مفعّل” حسب قواعد الدولة (قد يكون بعد تحقق قناة واحدة أو كلاهما).

Payload مقترح:

- **tenant_id**
- **user_id**
- **activated_at**
- **activation_rule**: `mobile_only | email_only | both | any_one`
- **requirements**: `{ username_required, national_id_required, mobile_required, email_required }`
- **verified**: `{ mobile_verified, email_verified }`

## خدمات مستقبلية يمكنها الاستماع

- **Notifications**: إرسال رسالة ترحيب/إرشادات بعد `created` أو `activated`.
- **Provisioning**: تجهيز بيانات أولية للـ Tenant بعد `created`.
- **Analytics**: تسجيل funnels ومعدلات التحويل بين `submitted` → `created` → `activated`.
- **RBAC**: (اختياري) إنشاء أدوار/صلاحيات افتراضية للـ Tenant بعد `created` (يرتبط بخدمة RBAC).

