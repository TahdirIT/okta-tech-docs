# مراجع خدمة إدارة الدول (Countries Management)

هذا الملف يحتوي على جميع المراجع والملفات والمجلدات المتعلقة بخدمة إدارة الدول عند كتابة prompt لأي AI agent.

---

## 📁 البنية الأساسية للمشروع

### المجلد الرئيسي
- `docs/services/contries-management/` - المجلد الرئيسي لخدمة إدارة الدول

---

## 📚 التوثيق الشامل (Guide)

**المجلد:** `docs/services/contries-management/guide/`

### الملفات الأساسية:
- `README.md` - الفهرس الرئيسي لملفات التوثيق
- `00-database-structure.md` - هيكل قاعدة البيانات الكامل
- `01-overview.md` - نظرة عامة على الميزة
- `02-feature-goal.md` - الهدف من الميزة
- `03-country-data.md` - بيانات الدولة
- `04-stages-management.md` - إدارة المراحل التعليمية
- `05-calendar.md` - إدارة التقويم
- `06-subjects-management.md` - إدارة المواد الدراسية
- `07-academic-years.md` - إدارة الأعوام الدراسية
- `08-notifications.md` - إدارة تعريفات الإشعارات
- `09-weekdays-settings.md` - إعدادات الأسبوع
- `10-regions-management.md` - إدارة المناطق

---

## 💻 التوثيق التقني (Tech)

**المجلد:** `docs/services/contries-management/tech/`

### الملفات الرئيسية:
- `permissions.md` - جميع الصلاحيات المطلوبة للميزة
- `__missing-files.md` - الملفات المفقودة التي تحتاج إلى إنشاء

### النماذج (Models)
**المجلد:** `docs/services/contries-management/tech/models/`

- `01-countries.md` - نموذج الدول
- `02-regions.md` - نموذج المناطق
- `03-cities.md` - نموذج المدن
- `04-districts.md` - نموذج الأحياء
- `05-academic_years.md` - نموذج الأعوام الدراسية
- `06-terms.md` - نموذج الفصول الدراسية
- `07-education_level_groups.md` - نموذج مجموعات المراحل التعليمية
- `08-education_levels.md` - نموذج المراحل التعليمية
- `09-education_level_group_levels.md` - نموذج ربط المراحل بالمجموعات
- `10-subjects.md` - نموذج المواد الدراسية
- `11-subject_education_levels.md` - نموذج ربط المواد بالمراحل
- `12-holiday_schedules.md` - نموذج جداول الإجازات
- `13-model_settings.md` - نموذج إعدادات النموذج
- `14-notification_definitions.md` - نموذج تعريفات الإشعارات
- `15-notifications.md` - نموذج الإشعارات
- `16-notification_receivers.md` - نموذج مستقبلي الإشعارات

---

## 🎨 تجربة المستخدم (User Experience)

**المجلد:** `docs/services/contries-management/user-experience/`

### الملفات:
- `README.md` - الفهرس الرئيسي لملفات تجربة المستخدم
- `01-country-data-ux.md` - تجربة المستخدم لبيانات الدولة
- `02-stages-management-ux.md` - تجربة المستخدم لإدارة المراحل
- `03-calendar-ux.md` - تجربة المستخدم للتقويم
- `04-subjects-management-ux.md` - تجربة المستخدم لإدارة المواد
- `05-academic-years-ux.md` - تجربة المستخدم للأعوام الدراسية
- `06-notifications-ux.md` - تجربة المستخدم للإشعارات
- `07-weekdays-settings-ux.md` - تجربة المستخدم لإعدادات الأسبوع
- `08-regions-management-ux.md` - تجربة المستخدم لإدارة المناطق

---

## 📋 المعايير التقنية العامة

**المجلد:** `docs/tech-standards/`

### الملفات:
- `README.md` - الفهرس الرئيسي للمعايير التقنية
- `design-standards.md` - معايير الهوية والتصميم
- `permissions-naming.md` - معيار تسمية أكواد الصلاحيات

---

## 📄 الملفات العامة في المشروع

**المجلد:** `docs/`

- `README.md` - نظرة عامة على المشروع
- `tenants.md` - معلومات عن المستأجرين (Tenants)
- `end-users.md` - معلومات عن المستخدمين النهائيين
- `packages.md` - معلومات عن الحزم
- `partner-platform.md` - معلومات عن منصة الشركاء
- `services/core-services.md` - الخدمات الأساسية

---

## 🎯 كيفية استخدام هذه المراجع

عند كتابة prompt لأي AI agent للعمل على خدمة إدارة الدول:

1. **للتوثيق الشامل:** ابدأ بقراءة `guide/01-overview.md` ثم الملفات الأخرى حسب الحاجة
2. **للنماذج والبنية التقنية:** راجع `tech/models/` و `tech/permissions.md`
3. **لتجربة المستخدم:** راجع `user-experience/` لفهم التدفقات والواجهات
4. **للمعايير:** راجع `tech-standards/` للتأكد من اتباع المعايير

---

## 📝 ملاحظات مهمة

- جميع الملفات مكتوبة باللغة العربية
- المشروع يستخدم Laravel مع Livewire (بدون API)
- يتم استخدام ULID للجداول التي تحتاجها
- يتم استخدام Soft Deletes حيث مطلوب
- يجب اتباع معايير التسمية في `tech-standards/permissions-naming.md`

---

## 🔗 الترتيب المقترح للقراءة

1. `guide/01-overview.md` - لفهم الميزة بشكل عام
2. `guide/02-feature-goal.md` - لفهم الهدف من الميزة
3. `guide/00-database-structure.md` - لفهم هيكل قاعدة البيانات
4. `tech/models/` - لفهم النماذج بالتفصيل
5. `user-experience/` - لفهم تجربة المستخدم
6. `tech/permissions.md` - لفهم الصلاحيات المطلوبة
