# الصلاحيات - Tenant Registration

تسجيل الكيان عادةً يكون متاحًا **بدون تسجيل دخول** (Public), لذلك غالبًا لا يتطلب صلاحيات داخلية.

## اعتبارات

- إن كان هناك “لوحة تسجيل” عامة: لا يوجد Authorization سوى Rate limiting ووسائل الحماية.
- إن كان التسجيل يُدار من داخل النظام (بواسطة موظف/مشرف): يمكن إضافة صلاحيات مثل:
  - `tenant_registration.create`
  - `tenant_registration.review`
  - `tenant_registration.approve` (إن وجد تدفق موافقة)

> ملاحظة: ربط الصلاحيات يُفضل أن يتبع خدمة RBAC:
> `docs/services/role-based-access-control/guide/01-overview.md`

