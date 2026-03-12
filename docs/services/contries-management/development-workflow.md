# خطوات العمل التطويرية - إدارة الدول

هذا الملف يوثق الخطوات التطويرية المطلوبة لبرمجة ميزة إدارة الدول داخل المنصة باستخدام Livewire بدون API.

---

## المرحلة الأولى: الإعداد والبنية الأساسية

### 1. إنشاء قاعدة البيانات (Database Migrations)

**الترتيب:**
1. إنشاء migration لجدول `countries` (النموذج الأساسي)
2. إنشاء migrations للجداول التابعة حسب الترتيب:
   - `regions` → `cities` → `districts`
   - `academic_years` → `terms`
   - `education_level_groups` → `education_levels` → `education_level_group_levels`
   - `subjects` → `subject_education_levels`
   - `holiday_schedules`
   - `model_settings`
   - `notification_definitions` → `notifications` → `notification_receivers`

**المرجع:** `guide/00-database-structure.md` و `tech/models/`

**ملاحظات:**
- استخدام ULID للجداول التي تحتاجها
- إضافة الفهارس والقيود (constraints) حسب المواصفات
- استخدام Soft Deletes حيث مطلوب

---

### 2. إنشاء النماذج (Models)

**الترتيب:** نفس ترتيب Migrations

**المهام:**
- إنشاء كل Model مع العلاقات (Relationships)
- إضافة Traits المطلوبة (SoftDeletes, HasUlid, إلخ)
- تعريف Accessors و Mutators إذا لزم الأمر
- إضافة Scopes الشائعة

**المرجع:** `tech/models/`

---

### 3. إنشاء Seeders للبيانات الأولية

**المهام:**
- إنشاء Seeder رئيسي يستدعي باقي Seeders
- إنشاء Seeders للبيانات التجريبية لكل جدول
- إضافة بيانات اختبارية واقعية لتسهيل التطوير

---

## المرحلة الثانية: الصلاحيات والأمان

### 4. إنشاء Policies

**الترتيب:** حسب أولوية الاستخدام:
1. `CountryPolicy` (الأساسي)
2. `RegionPolicy`, `CityPolicy`, `DistrictPolicy`
3. `AcademicYearPolicy`, `TermPolicy`
4. `EducationLevelPolicy`, `EducationLevelGroupPolicy`
5. `SubjectPolicy`
6. `HolidaySchedulePolicy`
7. `NotificationDefinitionPolicy`
8. باقي Policies حسب الحاجة

**المهام:**
- ربط كل Policy بصلاحيات الملف `tech/permissions.md`
- تنفيذ methods: `viewAny`, `view`, `create`, `update`, `delete`
- إضافة methods مخصصة مثل `activate` للدول

**المرجع:** `tech/permissions.md`

---

### 5. إنشاء Middleware للصلاحيات

**المهام:**
- إنشاء Middleware للتحقق من صلاحيات countries_management
- ربط Middleware بالمسارات (Routes)

---

## المرحلة الثالثة: منطق الأعمال (Services/Repositories)

### 6. إنشاء Services

**الترتيب:** حسب الأولوية الوظيفية:
1. `CountryService` - العمليات الأساسية للدول
2. `RegionService` - إدارة المناطق والمدن والأحياء
3. `AcademicYearService` - إدارة الأعوام والفصول
4. `EducationLevelService` - إدارة المراحل ومجموعاتها
5. `SubjectService` - إدارة المواد وربطها بالمراحل
6. `CalendarService` - إدارة التقويم والإجازات
7. `NotificationService` - إدارة تعريفات الإشعارات
8. `ConductRulesService` - إدارة قواعد السلوك والمواظبة

**المهام:**
- نقل منطق الأعمال المعقد من Components إلى Services
- تنفيذ قواعد التحقق المذكورة في `tech/permissions.md`
- معالجة العلاقات بين النماذج
- إضافة معالجة الأخطاء والاستثناءات

---

### 7. إنشاء Form Requests (Validation)

**الترتيب:** لكل عملية تحتاج تحقق:
- `StoreCountryRequest`, `UpdateCountryRequest`
- `StoreRegionRequest`, `UpdateRegionRequest`
- `StoreAcademicYearRequest`, `UpdateAcademicYearRequest`
- وهكذا لباقي النماذج

**المهام:**
- تنفيذ قواعد التحقق المذكورة في `tech/permissions.md`
- إضافة رسائل أخطاء بالعربية
- التحقق من الصلاحيات داخل Rules

---

## المرحلة الرابعة: مكونات Livewire

### 8. إنشاء Livewire Components - الأقسام الأساسية

**الترتيب حسب الأولوية:**

#### 8.1 بيانات الدولة (Country Data)
- `CountriesIndex` - عرض قائمة الدول
- `CountryForm` - نموذج إنشاء/تعديل دولة
- `CountryShow` - عرض تفاصيل دولة

**المرجع:** `user-experience/01-country-data-ux.md`

#### 8.2 إدارة المناطق (Regions Management)
- `RegionsIndex` - عرض الهيكل الجغرافي
- `RegionForm` - نموذج إدارة المناطق
- `CityForm` - نموذج إدارة المدن
- `DistrictForm` - نموذج إدارة الأحياء

**المرجع:** `user-experience/09-regions-management-ux.md`

#### 8.3 إدارة الأعوام الدراسية (Academic Years)
- `AcademicYearsIndex` - عرض الأعوام الدراسية
- `AcademicYearForm` - نموذج إدارة الأعوام
- `TermsIndex` - عرض الفصول الدراسية
- `TermForm` - نموذج إدارة الفصول

**المرجع:** `user-experience/05-academic-years-ux.md`

---

### 9. إنشاء Livewire Components - الأقسام المتوسطة

#### 9.1 إدارة المراحل (Stages Management)
- `EducationLevelsIndex` - عرض المراحل الدراسية
- `EducationLevelForm` - نموذج إدارة المراحل
- `EducationLevelGroupsIndex` - عرض مجموعات المراحل
- `EducationLevelGroupForm` - نموذج إدارة المجموعات

**المرجع:** `user-experience/02-stages-management-ux.md`

#### 9.2 إدارة المواد (Subjects Management)
- `SubjectsIndex` - عرض المواد الدراسية
- `SubjectForm` - نموذج إدارة المواد
- `SubjectEducationLevelsManager` - ربط المواد بالمراحل

**المرجع:** `user-experience/04-subjects-management-ux.md`

#### 9.3 التقويم (Calendar)
- `CalendarView` - عرض التقويم الدراسي
- `HolidaySchedulesIndex` - عرض الإجازات والأنشطة
- `HolidayScheduleForm` - نموذج إدارة الإجازات

**المرجع:** `user-experience/03-calendar-ux.md`

---

### 10. إنشاء Livewire Components - الأقسام المتقدمة

#### 10.1 إدارة تعريفات الإشعارات (Notifications)
- `NotificationDefinitionsIndex` - عرض التعريفات
- `NotificationDefinitionForm` - نموذج إدارة التعريفات
- `NotificationChannelsManager` - تكوين قنوات الإرسال
- `NotificationGroupsManager` - إدارة المجموعات

**المرجع:** `user-experience/06-notifications-ux.md`

#### 10.2 قواعد السلوك والمواظبة (Conduct Rules)
- `ConductRulesIndex` - عرض القواعد
- `ConductProblemGradesManager` - إدارة درجات المشكلات
- `ConductProblemsManager` - إدارة المشكلات السلوكية
- `ConductProceduresManager` - إدارة الإجراءات التربوية
- `AbsenceRulesManager` - إدارة قواعد الغياب

**المرجع:** `user-experience/07-conduct-rules-ux.md`

#### 10.3 إعدادات الأسبوع (Weekdays Settings)
- `WeekdaysSettingsForm` - نموذج إعدادات الأسبوع

**المرجع:** `user-experience/08-weekdays-settings-ux.md`

---

## المرحلة الخامسة: الواجهات (Views/Blade)

### 11. إنشاء Blade Templates

**الترتيب:** لكل Component من Components Livewire:
- إنشاء ملف Blade في `resources/views/livewire/countries-management/`
- استخدام مكونات Blade قابلة لإعادة الاستخدام
- تطبيق معايير التصميم من `tech-standards/design-standards.md`

**المهام:**
- إنشاء Layouts مشتركة
- إنشاء Components للجداول والنماذج
- إضافة JavaScript المطلوب للتفاعلات المعقدة
- تطبيق CSS المخصص حسب الحاجة

**المرجع:** `user-experience/` لجميع الأقسام

---

## المرحلة السادسة: المسارات والتنقل

### 12. تعريف Routes

**المهام:**
- إنشاء Route Group لـ `countries-management`
- ربط كل Component بمسار مناسب
- إضافة Middleware للصلاحيات
- تنظيم Routes حسب الأقسام

**البنية المقترحة:**
```
/countries-management/countries
/countries-management/regions
/countries-management/academic-years
/countries-management/stages
/countries-management/subjects
/countries-management/calendar
/countries-management/notifications
/countries-management/conduct-rules
/countries-management/weekdays
```

---

## المرحلة السابعة: الأحداث والتفاعلات

### 13. إنشاء Events & Listeners

**المهام:**
- إنشاء Events للأحداث المهمة:
  - `CountryCreated`, `CountryUpdated`, `CountryDeleted`
  - `AcademicYearActivated`, `TermActivated`
  - `HolidayScheduleCreated` (لإرسال الإشعارات)
- إنشاء Listeners للأحداث:
  - تحديث Cache
  - إرسال إشعارات
  - تسجيل في Audit Log

---

### 14. إنشاء Jobs للمهام المجدولة

**المهام:**
- إنشاء Jobs للمهام الثقيلة:
  - معالجة البيانات الكبيرة
  - إرسال الإشعارات الجماعية
  - تحديث الإحصائيات

---

## المرحلة الثامنة: الاختبارات

### 15. كتابة Tests

**الترتيب:**
1. Unit Tests للـ Services
2. Unit Tests للـ Policies
3. Feature Tests لمكونات Livewire
4. Integration Tests للعمليات الكاملة

**المهام:**
- تغطية السيناريوهات الأساسية
- تغطية حالات الخطأ والحدودية
- اختبار الصلاحيات والتحقق
- اختبار العلاقات بين النماذج

---

## المرحلة التاسعة: الترجمة والتحسينات

### 16. إضافة ملفات الترجمة

**المهام:**
- إنشاء ملفات اللغة في `lang/ar/countries-management.php`
- إضافة جميع النصوص المستخدمة
- رسائل النجاح والأخطاء
- تسميات الحقول والنماذج

---

### 17. التحسينات النهائية

**المهام:**
- تحسين الأداء (Eager Loading، Caching)
- إضافة Pagination للجداول الكبيرة
- تحسين تجربة المستخدم (Loading States، Confirmations)
- إضافة Search و Filtering المتقدم
- مراجعة الأمان والصلاحيات

---

## المرحلة العاشرة: المراجعة والتدقيق

### 18. Code Review

**التحقق من:**
- اتباع معايير الكود
- تطبيق قواعد الصلاحيات بشكل صحيح
- تغطية الاختبارات
- جودة الكود والأداء

---

### 19. التوثيق النهائي

**المهام:**
- مراجعة التوثيق التقني
- تحديث ملفات User Experience إذا لزم الأمر
- إضافة PHPDoc للكود المهم
- توثيق أي قرارات تقنية مهمة

---

## ملاحظات عامة

### استخدام أدوات البرمجة الذكية

- استخدام Codex أو Claude لإنشاء الكود الأولي
- مراجعة وتعديل الكود المولد حسب الحاجة
- التأكد من اتباع معايير المشروع

### الترتيب المنطقي

- البدء بالأساسيات (Database، Models)
- ثم الأمان (Policies، Permissions)
- ثم منطق الأعمال (Services)
- ثم الواجهات (Livewire، Views)
- وأخيراً التحسينات والاختبارات

### الأولويات

1. **عاجل:** بيانات الدولة، المناطق، الأعوام الدراسية
2. **مهم:** المراحل، المواد، التقويم
3. **متقدم:** الإشعارات، قواعد السلوك، إعدادات الأسبوع

---

## المراجع

- **الدليل الشامل:** `guide/`
- **المواصفات التقنية:** `tech/`
- **تجربة المستخدم:** `user-experience/`
- **معايير التصميم:** `../tech-standards/design-standards.md`
- **معايير الصلاحيات:** `../tech-standards/permissions-naming.md`
