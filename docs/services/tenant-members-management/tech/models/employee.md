# نموذج الموظف (Employee)

## الهدف

تمثيل الموظف كعضو داخل الجهة مع دعم:

- دور أساسي (Primary role) يحدد التصنيف الوظيفي الرئيسي (مثل معلم/إداري).
- أدوار إضافية (Extra roles) تسمح بتجميع صلاحيات متعددة على نفس الحساب.
- فصل العضوية عن الجهة دون حذف تاريخها.

## الحقول الأساسية (مفاهيمياً)

- `id`
- `user_id` (مرجع إلى User)

## العلاقات

- **belongsTo User**
- **belongsToMany Tenants** عبر pivot مثل `employee_tenant`
  - يحمل عادةً: `primary_role_id`, `type`, `job_title`, `released_at`
- **roles/permissions** عبر RBAC tenant-scoped

## قواعد العمل

- الموظف قد يملك أكثر من role داخل الجهة (تجميعي).
- يجب دعم كون الموظف “معلماً” و“إدارياً” معاً عبر:
  - role أساسي + roles إضافية
  - أو role مركب حسب سياسة RBAC

## أمثلة بيانات

```json
{
  "employee_id": 7001,
  "user": { "id": 9001, "name": "اسم الموظف" },
  "tenant_membership": {
    "tenant_id": 77,
    "primary_role_id": 12,
    "type": "teacher",
    "released_at": null
  },
  "roles": ["tenant_members.employees.view", "tenant_members.students.view"]
}
```

