# الصلاحيات (Permissions) — Tenant Members Management

يتبع هذا الملف معيار تسمية الصلاحيات:

- `docs/tech-standards/permissions-naming.md`

صيغة الكود:

`<feature>.<resource>.<action>`

حيث feature المقترح هنا: `tenant_members_management`

## أدوار معنية (Roles)

- **Tenant Admin**: إدارة الطلاب/الأولياء/الموظفين/الأدوار/الاستيراد.
- **Staff/Teacher**: صلاحيات قراءة محددة (حسب سياسة الجهة).
- **System Admin**: تهيئة مخططات ملفات الاستيراد على مستوى النظام/الدولة.

## أكواد صلاحيات مقترحة

### 1) الطلاب

- `tenant_members_management.students.view`
- `tenant_members_management.students.create`
- `tenant_members_management.students.update`
- `tenant_members_management.students.unlink`
- `tenant_members_management.students.move_section`

### 2) أولياء الأمور

- `tenant_members_management.guardians.view`
- `tenant_members_management.guardians.create`
- `tenant_members_management.guardians.update`
- `tenant_members_management.guardians.link_student`
- `tenant_members_management.guardians.unlink_student`

### 3) الموظفون

- `tenant_members_management.employees.view`
- `tenant_members_management.employees.create`
- `tenant_members_management.employees.update`
- `tenant_members_management.employees.unlink`
- `tenant_members_management.employees.change_password`

### 4) أدوار الموظفين داخل الجهة

- `tenant_members_management.employee_roles.view`
- `tenant_members_management.employee_roles.create`
- `tenant_members_management.employee_roles.update`
- `tenant_members_management.employee_roles.delete`
- `tenant_members_management.employee_roles.assign_permissions`

### 5) الاستيراد

- `tenant_members_management.import.students`
- `tenant_members_management.import.guardians`
- `tenant_members_management.import.employees`

### 6) تهيئة مخططات الملفات (System-admin)

> هذه صلاحيات system-level؛ قد تكون ضمن خدمة “settings-management” أو “countries-management” حسب تقسيم المنتج، لكن ندرجها هنا لأنها شرط تشغيلي لخدمة الاستيراد.

- `tenant_members_management.file_formats.view`
- `tenant_members_management.file_formats.update`
- `tenant_members_management.file_formats.download_templates`

## قواعد تفويض (Authorization Rules)

- كل عمليات الكتابة (Create/Update/Unlink/Import) تتطلب:
  - User authenticated
  - Tenant context محدد (tenant_id)
  - Permission matching resource/action ضمن نفس tenant

## أمثلة

### 1) حماية Route / Endpoint

```txt
GET  /tenant/members/students     requires tenant_members_management.students.view
POST /tenant/members/students     requires tenant_members_management.students.create
POST /tenant/members/import       requires tenant_members_management.import.students
```

### 2) رد عدم التوافر

```json
{ "message": "This action is unauthorized." }
```

