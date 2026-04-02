# نموذج الفصل (Section / Class)

## الهدف

تعريف فصل داخل صف/مرحلة محددة داخل الجهة، وهو وحدة الربط الإلزامية للطالب.

## الحقول الأساسية (مفاهيمياً)

- `id`
- `tenant_id`
- `stage_id`
- `name`
- `order`

## العلاقات

- **belongsTo Tenant**
- **belongsTo Stage**
- **belongsToMany Students** (History)

## قواعد العمل

- يجب أن يكون `stage_id` صالحاً ضمن نفس الجهة.
- ربط الطالب يتم عبر:
  - مؤشر نشط `active_section_id` (على الطالب) + سجل علاقة تاريخي (Pivot).

