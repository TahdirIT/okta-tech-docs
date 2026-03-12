# الصلاحيات والقواعد - إدارة الدول

هذا الملف يحتوي على أكواد الصلاحيات والقواعد المتعلقة بخدمة **إدارة الدول**، منظمة حسب البنية التالية:

**countries_management -> sub_feature_management -> action**

---

## 1. بيانات الدولة (Country Data)

### الصلاحيات

- `countries_management.country_data.view` - عرض بيانات الدولة
- `countries_management.country_data.create` - إنشاء دولة جديدة
- `countries_management.country_data.update` - تعديل بيانات الدولة
- `countries_management.country_data.delete` - حذف دولة
- `countries_management.country_data.activate` - تفعيل/إيقاف الدولة

### القواعد

- يجب التحقق من عدم تكرار رمز الدولة (`code`) عند الإنشاء
- يجب التحقق من صحة رمز الهاتف الدولي (`phone_code`)
- يجب التحقق من صحة المنطقة الزمنية (`timezone`)
- لا يمكن حذف دولة مرتبطة بمدارس أو جهات تعليمية

---

## 2. إدارة المراحل (Stages Management)

### الصلاحيات

- `countries_management.stages.view` - عرض المراحل الدراسية
- `countries_management.stages.create` - إنشاء مرحلة دراسية جديدة
- `countries_management.stages.update` - تعديل مرحلة دراسية
- `countries_management.stages.delete` - حذف مرحلة دراسية

### مجموعات المراحل (Education Level Groups)

- `countries_management.stages.groups.view` - عرض مجموعات المراحل
- `countries_management.stages.groups.create` - إنشاء مجموعة مراحل جديدة
- `countries_management.stages.groups.update` - تعديل مجموعة مراحل
- `countries_management.stages.groups.delete` - حذف مجموعة مراحل
- `countries_management.stages.groups.assign_stages` - ربط المراحل بالمجموعة

### القواعد

- يجب التحقق من عدم تكرار اسم المرحلة داخل نفس الدولة
- يجب التحقق من صحة ترتيب المرحلة ضمن التسلسل الدراسي
- لا يمكن حذف مرحلة مرتبطة بصفوف أو مواد دراسية
- يجب التحقق من عدم تكرار اسم مجموعة المراحل داخل نفس الدولة

---

## 3. التقويم (Calendar)

### الصلاحيات

- `countries_management.calendar.view` - عرض التقويم الدراسي
- `countries_management.calendar.manage` - إدارة التقويم الدراسي

### جدول الإجازات والأنشطة (Holiday Schedule)

- `countries_management.calendar.holidays.view` - عرض جدول الإجازات والأنشطة
- `countries_management.calendar.holidays.create` - إنشاء إجازة/نشاط جديد
- `countries_management.calendar.holidays.update` - تعديل إجازة/نشاط
- `countries_management.calendar.holidays.delete` - حذف إجازة/نشاط

### القواعد

- يجب أن يكون تاريخ النهاية بعد أو يساوي تاريخ البداية
- يجب التحقق من عدم تداخل فترات الإجازات ضمن نفس النطاق الزمني
- يجب التحقق من صحة موعد إرسال الإشعارات (`send_notifications_at`) إذا كان الإشعار مفعلاً

---

## 4. إدارة المواد (Subjects Management)

### الصلاحيات

- `countries_management.subjects.view` - عرض المواد الدراسية
- `countries_management.subjects.create` - إنشاء مادة دراسية جديدة
- `countries_management.subjects.update` - تعديل مادة دراسية
- `countries_management.subjects.delete` - حذف مادة دراسية
- `countries_management.subjects.assign_stages` - ربط المواد بالمراحل

### القواعد

- يجب التحقق من عدم تكرار اسم المادة داخل نفس الدولة والمرحلة
- يجب التحقق من صحة ربط المادة بالمرحلة المناسبة
- لا يمكن حذف مادة مرتبطة بخطط دراسية أو جداول
- يجب التحقق من صحة الدرجة النهائية أو الوزن التقييمي

---

## 5. إدارة الأعوام الدراسية (Academic Years)

### الصلاحيات

- `countries_management.academic_years.view` - عرض الأعوام الدراسية
- `countries_management.academic_years.create` - إنشاء عام دراسي جديد
- `countries_management.academic_years.update` - تعديل عام دراسي
- `countries_management.academic_years.delete` - حذف عام دراسي
- `countries_management.academic_years.activate` - تفعيل/إيقاف عام دراسي

### الفصول الدراسية (Terms)

- `countries_management.academic_years.terms.view` - عرض الفصول الدراسية
- `countries_management.academic_years.terms.create` - إنشاء فصل دراسي جديد
- `countries_management.academic_years.terms.update` - تعديل فصل دراسي
- `countries_management.academic_years.terms.delete` - حذف فصل دراسي
- `countries_management.academic_years.terms.set_active` - تعيين الفصل النشط

### القواعد

- يجب أن يكون تاريخ نهاية العام بعد تاريخ البداية
- يجب التحقق من عدم تداخل الأعوام الدراسية في نفس الفترة الزمنية
- يجب التحقق من أن الفصول الدراسية تقع ضمن نطاق العام الدراسي
- لا يمكن حذف عام دراسي نشط
- يجب التحقق من وجود فصل نشط واحد فقط على مستوى الدولة

---

## 6. إدارة تعريفات الإشعارات (Notifications)

### الصلاحيات

- `countries_management.notifications.view` - عرض تعريفات الإشعارات
- `countries_management.notifications.create` - إنشاء تعريف إشعار جديد
- `countries_management.notifications.update` - تعديل تعريف إشعار
- `countries_management.notifications.delete` - حذف تعريف إشعار

### المجموعات (Groups)

- `countries_management.notifications.groups.view` - عرض مجموعات الإشعارات
- `countries_management.notifications.groups.manage` - إدارة مجموعات الإشعارات

### قنوات الإرسال (Channels)

- `countries_management.notifications.channels.configure` - تكوين قنوات الإرسال (app/watsi/sms)
- `countries_management.notifications.channels.set_status` - تعيين حالة القناة (forced/active/inactive)

### القواعد

- يجب التحقق من صحة صيغة المعرف (Slug) بصيغة `groupSlug.definitionSlug`
- يجب التحقق من عدم تكرار المعرف داخل نفس الدولة
- يجب التحقق من صحة المتغيرات (`variables`) المستخدمة في المحتوى
- يجب التحقق من أن حالة القناة واحدة من: `forced`, `active`, `inactive`

---

## 7. قواعد السلوك والمواظبة (Conduct Rules)

### الصلاحيات

- `countries_management.conduct_rules.view` - عرض قواعد السلوك والمواظبة
- `countries_management.conduct_rules.create` - إنشاء سجل قواعد جديد
- `countries_management.conduct_rules.update` - تعديل سجل قواعد
- `countries_management.conduct_rules.delete` - حذف سجل قواعد

### مجموعات الدرجات (Conduct Problem Grade Groups)

- `countries_management.conduct_rules.grade_groups.view` - عرض مجموعات الدرجات
- `countries_management.conduct_rules.grade_groups.create` - إنشاء مجموعة درجات جديدة
- `countries_management.conduct_rules.grade_groups.update` - تعديل مجموعة درجات
- `countries_management.conduct_rules.grade_groups.delete` - حذف مجموعة درجات

### درجات المشكلات (Conduct Problem Grades)

- `countries_management.conduct_rules.problem_grades.view` - عرض درجات المشكلات
- `countries_management.conduct_rules.problem_grades.create` - إنشاء درجة مشكلة جديدة
- `countries_management.conduct_rules.problem_grades.update` - تعديل درجة مشكلة
- `countries_management.conduct_rules.problem_grades.delete` - حذف درجة مشكلة

### المشكلات السلوكية (Conduct Problems)

- `countries_management.conduct_rules.problems.view` - عرض المشكلات السلوكية
- `countries_management.conduct_rules.problems.create` - إنشاء مشكلة سلوكية جديدة
- `countries_management.conduct_rules.problems.update` - تعديل مشكلة سلوكية
- `countries_management.conduct_rules.problems.delete` - حذف مشكلة سلوكية
- `countries_management.conduct_rules.problems.assign_grade` - ربط المشكلة بدرجة

### الإجراءات التربوية (Conduct Educational Procedures)

- `countries_management.conduct_rules.procedures.view` - عرض الإجراءات التربوية
- `countries_management.conduct_rules.procedures.create` - إنشاء إجراء تربوي جديد
- `countries_management.conduct_rules.procedures.update` - تعديل إجراء تربوي
- `countries_management.conduct_rules.procedures.delete` - حذف إجراء تربوي
- `countries_management.conduct_rules.procedures.assign_grade` - ربط الإجراء بدرجة

### قواعد الغياب (Absence Rules)

- `countries_management.conduct_rules.absence_rules.view` - عرض قواعد الغياب
- `countries_management.conduct_rules.absence_rules.create` - إنشاء قاعدة غياب جديدة
- `countries_management.conduct_rules.absence_rules.update` - تعديل قاعدة غياب
- `countries_management.conduct_rules.absence_rules.delete` - حذف قاعدة غياب

### إجراءات الغياب (Absence Procedures)

- `countries_management.conduct_rules.absence_procedures.view` - عرض إجراءات الغياب
- `countries_management.conduct_rules.absence_procedures.create` - إنشاء إجراء غياب جديد
- `countries_management.conduct_rules.absence_procedures.update` - تعديل إجراء غياب
- `countries_management.conduct_rules.absence_procedures.delete` - حذف إجراء غياب
- `countries_management.conduct_rules.absence_procedures.assign_rule` - ربط الإجراء بقاعدة غياب

### القواعد

- يجب التحقق من عدم تكرار اسم السجل داخل نفس الدولة
- يجب التحقق من صحة ربط المشكلات والإجراءات بالدرجات المناسبة
- يجب التحقق من صحة شروط قواعد الغياب (مثل عدد الأيام)
- لا يمكن حذف قاعدة أو إجراء مرتبط بسجلات سلوكية فعلية

---

## 8. إعدادات الأسبوع (Weekdays Settings)

### الصلاحيات

- `countries_management.weekdays.view` - عرض إعدادات الأسبوع
- `countries_management.weekdays.update` - تعديل إعدادات الأسبوع

### القواعد

- يجب تحديد أيام الدراسة وأيام نهاية الأسبوع بشكل واضح
- يجب التحقق من أن أيام الدراسة لا تتداخل مع أيام نهاية الأسبوع
- يجب التحقق من وجود يوم واحد على الأقل كعطلة أسبوعية

---

## 9. إدارة المناطق (Regions Management)

### الصلاحيات

- `countries_management.regions.view` - عرض المناطق
- `countries_management.regions.create` - إنشاء منطقة جديدة
- `countries_management.regions.update` - تعديل منطقة
- `countries_management.regions.delete` - حذف منطقة

### المدن (Cities)

- `countries_management.regions.cities.view` - عرض المدن
- `countries_management.regions.cities.create` - إنشاء مدينة جديدة
- `countries_management.regions.cities.update` - تعديل مدينة
- `countries_management.regions.cities.delete` - حذف مدينة

### الأحياء (Districts)

- `countries_management.regions.districts.view` - عرض الأحياء
- `countries_management.regions.districts.create` - إنشاء حي جديد
- `countries_management.regions.districts.update` - تعديل حي
- `countries_management.regions.districts.delete` - حذف حي

### القواعد

- يجب التحقق من عدم تكرار اسم المنطقة داخل نفس الدولة
- يجب التحقق من عدم تكرار اسم المدينة داخل نفس المنطقة
- يجب التحقق من عدم تكرار اسم الحي داخل نفس المدينة
- يجب التحقق من صحة الرقم الوطني (`national_id`) إن وجد
- لا يمكن حذف منطقة/مدينة/حي مرتبطة بمدارس أو جهات تعليمية

---

## ملاحظات عامة

### صلاحيات الإدارة الشاملة

- `countries_management.*` - جميع الصلاحيات المتعلقة بإدارة الدول (صلاحية رئيسية)
- `countries_management.*.view` - صلاحية عرض جميع الميزات
- `countries_management.*.manage` - صلاحية إدارة شاملة لجميع الميزات

### القواعد العامة

- جميع العمليات تتطلب التحقق من صلاحيات المستخدم
- يجب التحقق من وجود الدولة قبل تنفيذ أي عملية متعلقة بها
- يجب التحقق من حالة التفعيل (`active`) للدولة قبل تنفيذ بعض العمليات
- يجب تسجيل جميع عمليات الإنشاء والتعديل والحذف في سجل التدقيق (Audit Log)
