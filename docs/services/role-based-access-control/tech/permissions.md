# الصلاحيات والقواعد - إدارة الصلاحيات والأدوار

هذا الملف يحتوي على أكواد الصلاحيات والقواعد المتعلقة بخدمة **إدارة الصلاحيات والأدوار**، منظمة حسب البنية التالية:

**permissions_and_roles_management -> feature -> action**

---

## 1. إدارة الصلاحيات (Permissions Management)

### الصلاحيات

- `permissions_and_roles_management.permissions.view` - عرض قائمة الصلاحيات
- `permissions_and_roles_management.permissions.create` - إنشاء صلاحية جديدة
- `permissions_and_roles_management.permissions.update` - تعديل صلاحية
- `permissions_and_roles_management.permissions.delete` - حذف صلاحية
- `permissions_and_roles_management.permissions.scan` - مسح الكود لاكتشاف الصلاحيات المفقودة
- `permissions_and_roles_management.permissions.import` - استيراد الصلاحيات من الكود

### القواعد

- يجب التحقق من عدم تكرار اسم الصلاحية ضمن نفس `guard_name` و `scope`
- يجب التحقق من أن النطاق (`scope`) واحد من: `tenant`, `system`
- لا يمكن حذف صلاحية مرتبطة بأدوار أو مستخدمين
- يجب التحقق من صحة اسم الصلاحية (لا يحتوي على أحرف خاصة غير مسموحة)

---

## 2. إدارة الأدوار (Roles Management)

### الصلاحيات

- `permissions_and_roles_management.roles.view` - عرض قائمة الأدوار
- `permissions_and_roles_management.roles.create` - إنشاء دور جديد
- `permissions_and_roles_management.roles.update` - تعديل دور
- `permissions_and_roles_management.roles.delete` - حذف دور
- `permissions_and_roles_management.roles.assign_permissions` - ربط الصلاحيات بالدور
- `permissions_and_roles_management.roles.scan` - مسح الكود لاكتشاف الأدوار المفقودة
- `permissions_and_roles_management.roles.import` - استيراد الأدوار من الكود

### القواعد

- يجب التحقق من عدم تكرار اسم الدور ضمن نفس `tenant_id` و `guard_name`
- يجب التحقق من أن النطاق (`scope`) واحد من: `tenant`, `system`
- لا يمكن حذف دور مرتبط بمستخدمين
- يجب التحقق من صحة اسم الدور (لا يحتوي على أحرف خاصة غير مسموحة)
- يجب التحقق من وجود الصلاحيات المراد ربطها بالدور قبل الربط

---

## 3. مسح واستيراد الصلاحيات والأدوار (RBAC Discovery)

### الصلاحيات

- `permissions_and_roles_management.rbac.scan` - مسح الكود لاكتشاف الصلاحيات والأدوار المفقودة
- `permissions_and_roles_management.rbac.import_permissions` - استيراد الصلاحيات المفقودة
- `permissions_and_roles_management.rbac.import_roles` - استيراد الأدوار المفقودة
- `permissions_and_roles_management.rbac.view_report` - عرض تقرير الصلاحيات والأدوار المفقودة

### القواعد

- يجب التحقق من وجود ملف التقرير قبل عرضه
- يجب التحقق من صحة بيانات التقرير قبل الاستيراد
- يجب التحقق من النطاق (`scope`) المحدد عند الاستيراد
- يجب تسجيل جميع عمليات المسح والاستيراد في سجل التدقيق (Audit Log)

---

## ملاحظات عامة

### صلاحيات الإدارة الشاملة

- `permissions_and_roles_management.*` - جميع الصلاحيات المتعلقة بإدارة الصلاحيات والأدوار (صلاحية رئيسية)
- `permissions_and_roles_management.*.view` - صلاحية عرض جميع الميزات
- `permissions_and_roles_management.*.manage` - صلاحية إدارة شاملة لجميع الميزات

### القواعد العامة

- جميع العمليات تتطلب التحقق من صلاحيات المستخدم
- يجب التحقق من وجود الصلاحية أو الدور قبل تنفيذ أي عملية متعلقة بها
- يجب التحقق من النطاق (`scope`) قبل تنفيذ بعض العمليات
- يجب تسجيل جميع عمليات الإنشاء والتعديل والحذف في سجل التدقيق (Audit Log)
- الصلاحيات والأدوار منفصلة تماماً ويمكن إدارتها بشكل مستقل
