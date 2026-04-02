# العلاقات (Relationships & Pivots)

هذا الملف يوحد توصيف العلاقات التي تعتمد عليها الخدمة لإدارة الربط/الفصل مع حفظ التاريخ.

## 1) Student ↔ Tenant (Membership)

### الهدف

تمثيل أن الطالب “عضو” داخل جهة (Tenant) مع إمكانية الفصل دون حذف السجل.

### حقول Pivot مقترحة

- `tenant_id`
- `student_id`
- `released_at` (nullable): تاريخ فصل الطالب من الجهة
- `created_at`, `updated_at`

### قواعد

- **Active membership**: العلاقة الفعّالة هي التي `released_at = null`.
- فصل الطالب: تحديث `released_at` بدل حذف السجل.

## 2) Student ↔ Section (Academic placement)

### حقول Pivot مقترحة

- `section_id`
- `student_id`
- `type` (مثال: regular/affiliate) إن كانت حالة الطالب مرتبطة بالفصل
- `released_at` (nullable)
- `created_at`, `updated_at`

### قواعد

- الطالب يجب أن يملك Section فعّال داخل الجهة طالما هو مرتبط بها.
- نقل الطالب: release للفصل السابق + attach للفصل الجديد + تحديث `active_section_id`.

## 3) Guardian ↔ Student

### حقول Pivot مقترحة

- `guardian_id`
- `student_id`
- `unlinked_at` (nullable)
- `created_at`, `updated_at`

### قواعد

- فصل ولي الأمر عن طالب: تحديث `unlinked_at`.
- يمكن لولي الأمر ربط أكثر من طالب.

## 4) Employee ↔ Tenant

### حقول Pivot مقترحة

- `employee_id`
- `tenant_id`
- `primary_role_id` (nullable حسب سياسة RBAC)
- `type` (مثال: teacher/administrator)
- `job_title` (nullable)
- `released_at` (nullable)
- `created_at`, `updated_at`

### قواعد

- العلاقة الفعّالة: `released_at = null`.
- فصل الموظف: release + (اختياري) تنظيف roles tenant-scoped حسب السياسة.

