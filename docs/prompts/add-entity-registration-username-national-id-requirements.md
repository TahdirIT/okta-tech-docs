# إضافة: إعدادات إلزام Username + National ID في تخصيصات تسجيل الكيان

هذا الملف عبارة عن **مقطع جاهز** يمكن نسخه ولصقه داخل prompt (مثال: Claude) عند العمل على إعدادات **Entity Registration Customizations** ضمن خدمة إدارة الدول فقط.

## النطاق (Scope)

- التعديلات داخل: `docs/services/contries-management/` فقط.
- لا تعدل أي ملفات خارج هذا المسار.
- لا تضف أو تعدل أي شيء في `tenant-registration` أو أي خدمة أخرى.

## السياق والمراجع التي يجب على الـ AI قراءتها أولًا

- `docs/services/contries-management/guide/entity-registration-customizations.md`
- `docs/services/contries-management/user-experience/entity-registration-customizations-ux.md`
- `docs/services/contries-management/tech/data-handling/entity_registration_customizations.md`

## Prompt snippet (جاهز لـ Claude)

```text
أضف دعم إعدادات إلزام الحقول التالية ضمن contact_requirements في تخصيصات تسجيل الكيان على مستوى الدولة:
- username_required
- national_id_required

المطلوب:
1) تحديث الدليل الوظيفي (guide) لتوضيح أن Username و National ID قابلان للإلزام حسب الدولة.
2) تحديث UX لعرض إعدادات إلزام الحقلين ضمن شاشة التخصيصات.
3) تحديث tech/data-handling schema بحيث يحتوي contact_requirements على:
   - username_required: boolean
   - national_id_required: boolean
   (مع الحفاظ على بقية الحقول الموجودة إن كانت مستخدمة).
4) تحديث أمثلة JSON في نفس ملفات contries-management بحيث تعكس الحقول الجديدة.
5) الحفاظ على اتساق المصطلحات بين guide و UX و tech (Username / National ID).

قيود مهمة:
- نطاق التعديل محصور في docs/services/contries-management فقط.
- لا تعدل tenant-registration.
- لا تغيّر بنية غير مرتبطة بهذه الإضافة.
```

