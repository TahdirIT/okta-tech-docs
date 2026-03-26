# إضافة: Validations في تخصيصات تسجيل الكيان (Entity Registration Customizations)

هذا الملف عبارة عن **مقطع جاهز** يمكن نسخه ولصقه داخل prompt (مثال: Claude) عند العمل على ميزة **تخصيصات تسجيل الكيان** ضمن خدمة إدارة الدول.

## السياق والمراجع التي يجب على الـ AI قراءتها أولًا

- `docs/services/contries-management/guide/entity-registration-customizations.md`
- `docs/services/contries-management/user-experience/entity-registration-customizations-ux.md`
- `docs/services/contries-management/tech/data-handling/entity_registration_customizations.md`

## Prompt snippet (جاهز لـ Claude)

```text
اعتبر أن تعريف custom field يدعم كائن validations اختياري.

- Multiple Regex verifications:
  - validations.regex_rules: array
  - لكل عنصر: { regex: string, message: { ar: string, en: string } }
  - تُطبّق القواعد بالترتيب، وأول قاعدة تفشل ترجع رسالة خطئها حسب لغة الواجهة.

- Limits validations حسب النوع داخل validations:
  - text/textarea: min_length, max_length
  - number: min, max
  - date: min_date, max_date (YYYY-MM-DD)
  - file: min_size_mb (optional), max_size_mb
  - multi_select/checkbox_group (optional): min_selected, max_selected

ملاحظات تنفيذية/تحقق:
- تحقق من الحدود غير المنطقية (min>max, min_length>max_length, min_date>max_date).
- تحقق من Regex غير صالح عند الحفظ.
- عند فشل regex_rules أثناء الإدخال: اعرض message.ar أو message.en حسب لغة الواجهة.
```

