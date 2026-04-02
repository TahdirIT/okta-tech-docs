# نموذج الطالب (Student)

## الهدف

تمثيل الطالب كعضو داخل الجهة (Tenant). الطالب يعتمد على:

- **User**: الهوية العامة (الاسم/الهوية/الهاتف/…)
- **Tenant membership**: ربطه بجهة فعّالة
- **Academic placement**: ربطه بفصل (Section) فعّال داخل الجهة

## الحقول الأساسية (مفاهيمياً)

- `id`
- `user_id` (مرجع إلى User)
- `active_tenant_id` (الجهة النشطة للطالب)
- `active_section_id` (الفصل النشط للطالب داخل الجهة)
- `active_status` (مثال: regular / affiliate)

> ملاحظة: أسماء الحقول في قاعدة البيانات قد تختلف، لكن المعنى يجب أن يبقى ثابتاً.

## العلاقات

- **belongsTo User**
- **belongsTo Tenant** (Active)
- **belongsTo Section** (Active)
- **belongsToMany Sections** (History)
- **belongsToMany Tenants** (History)
- **belongsToMany Guardians** (عبر علاقة guardian_student)

## قواعد العمل (Business Rules)

- **إلزام الصف/الفصل**: لا يمكن اعتبار الطالب “مرتبطاً” بالجهة بدون `active_section_id` صالح.
- **عضوية واحدة فعّالة**: لا يجب أن يكون للطالب أكثر من جهة فعّالة في نفس الوقت (حسب سياسة المنصة).
- **تاريخ الربط**: نقل الطالب أو فصله لا يحذف الروابط التاريخية، بل يغلقها بعلامة Release.

## أمثلة بيانات

### Student (API مثال)

```json
{
  "id": 101,
  "user": {
    "id": 5501,
    "name": "اسم الطالب",
    "national_id": "1234567890"
  },
  "active_tenant_id": 77,
  "active_section_id": 9003,
  "active_status": "regular"
}
```

