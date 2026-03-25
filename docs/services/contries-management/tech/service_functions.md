# وظائف المستخدم (Use-cases) — Countries Management

هذا المجلد يوثق **Use-cases** التي يقوم بها المستخدم داخل ميزة **إدارة الدول**، بصيغة متوافقة مع معيار تنظيم Feature Services:

- `docs/tech-standards/laravel-feature-services-structure.md`

صيغة المسارات المقترحة:

`app/Services/CountriesManagement/<Resource>/<Function>.php`

> ملاحظة: العناوين أدناه تصف ما يفعله المستخدم وظيفيًا، و"مكان الملف" هو مسار مقترح لملف الـService (Use-case class) في Laravel.

## الفهرس

- [1) Country Data](#1-country-data)
- [2) Regions / Cities / Districts](#2-regions--cities--districts)
- [3) Calendar (Academic Years / Terms / Holidays)](#3-calendar-academic-years--terms--holidays)
- [4) Subjects](#4-subjects)
- [5) Notifications](#5-notifications)
- [6) Weekdays Settings](#6-weekdays-settings)
- [7) Entity Registration Customizations](#7-entity-registration-customizations)

---

## 1) Country Data

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض قائمة الدول | `app/Services/CountriesManagement/Countries/ListCountries.php` |
| عرض تفاصيل دولة | `app/Services/CountriesManagement/Countries/ShowCountry.php` |
| إنشاء دولة | `app/Services/CountriesManagement/Countries/CreateCountry.php` |
| تحديث بيانات دولة | `app/Services/CountriesManagement/Countries/UpdateCountry.php` |
| حذف دولة | `app/Services/CountriesManagement/Countries/DeleteCountry.php` |
| تفعيل/إيقاف دولة | `app/Services/CountriesManagement/Countries/ToggleCountryActive.php` |

---

## 2) Regions / Cities / Districts

### Regions

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض مناطق دولة | `app/Services/CountriesManagement/Regions/ListRegions.php` |
| عرض تفاصيل منطقة | `app/Services/CountriesManagement/Regions/ShowRegion.php` |
| إنشاء منطقة | `app/Services/CountriesManagement/Regions/CreateRegion.php` |
| تحديث منطقة | `app/Services/CountriesManagement/Regions/UpdateRegion.php` |
| حذف منطقة | `app/Services/CountriesManagement/Regions/DeleteRegion.php` |

### Cities

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض مدن منطقة | `app/Services/CountriesManagement/Cities/ListCities.php` |
| عرض تفاصيل مدينة | `app/Services/CountriesManagement/Cities/ShowCity.php` |
| إنشاء مدينة | `app/Services/CountriesManagement/Cities/CreateCity.php` |
| تحديث مدينة | `app/Services/CountriesManagement/Cities/UpdateCity.php` |
| حذف مدينة | `app/Services/CountriesManagement/Cities/DeleteCity.php` |

### Districts

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض أحياء مدينة | `app/Services/CountriesManagement/Districts/ListDistricts.php` |
| عرض تفاصيل حي | `app/Services/CountriesManagement/Districts/ShowDistrict.php` |
| إنشاء حي | `app/Services/CountriesManagement/Districts/CreateDistrict.php` |
| تحديث حي | `app/Services/CountriesManagement/Districts/UpdateDistrict.php` |
| حذف حي | `app/Services/CountriesManagement/Districts/DeleteDistrict.php` |

---

## 3) Calendar (Academic Years / Terms / Holidays)

### Academic Years

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض الأعوام الدراسية | `app/Services/CountriesManagement/AcademicYears/ListAcademicYears.php` |
| عرض تفاصيل عام دراسي | `app/Services/CountriesManagement/AcademicYears/ShowAcademicYear.php` |
| إنشاء عام دراسي | `app/Services/CountriesManagement/AcademicYears/CreateAcademicYear.php` |
| تحديث عام دراسي | `app/Services/CountriesManagement/AcademicYears/UpdateAcademicYear.php` |
| حذف عام دراسي | `app/Services/CountriesManagement/AcademicYears/DeleteAcademicYear.php` |
| تفعيل/إيقاف عام دراسي | `app/Services/CountriesManagement/AcademicYears/ToggleAcademicYearActive.php` |

### Terms

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض فصول عام دراسي | `app/Services/CountriesManagement/Terms/ListTerms.php` |
| عرض تفاصيل فصل | `app/Services/CountriesManagement/Terms/ShowTerm.php` |
| إنشاء فصل | `app/Services/CountriesManagement/Terms/CreateTerm.php` |
| تحديث فصل | `app/Services/CountriesManagement/Terms/UpdateTerm.php` |
| حذف فصل | `app/Services/CountriesManagement/Terms/DeleteTerm.php` |
| تعيين الفصل النشط (على مستوى الدولة) | `app/Services/CountriesManagement/Terms/SetActiveTerm.php` |

### Holiday Schedules

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض جدول الإجازات/الأنشطة | `app/Services/CountriesManagement/HolidaySchedules/ListHolidaySchedules.php` |
| عرض تفاصيل إجازة/نشاط | `app/Services/CountriesManagement/HolidaySchedules/ShowHolidaySchedule.php` |
| إنشاء إجازة/نشاط | `app/Services/CountriesManagement/HolidaySchedules/CreateHolidaySchedule.php` |
| تحديث إجازة/نشاط | `app/Services/CountriesManagement/HolidaySchedules/UpdateHolidaySchedule.php` |
| حذف إجازة/نشاط | `app/Services/CountriesManagement/HolidaySchedules/DeleteHolidaySchedule.php` |

---

## 4) Subjects

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض المواد | `app/Services/CountriesManagement/Subjects/ListSubjects.php` |
| عرض تفاصيل مادة | `app/Services/CountriesManagement/Subjects/ShowSubject.php` |
| إنشاء مادة | `app/Services/CountriesManagement/Subjects/CreateSubject.php` |
| تحديث مادة | `app/Services/CountriesManagement/Subjects/UpdateSubject.php` |
| حذف مادة | `app/Services/CountriesManagement/Subjects/DeleteSubject.php` |
| ربط مادة بالمراحل/المستويات | `app/Services/CountriesManagement/Subjects/AssignSubjectEducationLevels.php` |

---

## 5) Notifications

### Notification Definitions

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض تعريفات الإشعارات | `app/Services/CountriesManagement/NotificationDefinitions/ListNotificationDefinitions.php` |
| عرض تفاصيل تعريف إشعار | `app/Services/CountriesManagement/NotificationDefinitions/ShowNotificationDefinition.php` |
| إنشاء تعريف إشعار | `app/Services/CountriesManagement/NotificationDefinitions/CreateNotificationDefinition.php` |
| تحديث تعريف إشعار | `app/Services/CountriesManagement/NotificationDefinitions/UpdateNotificationDefinition.php` |
| حذف تعريف إشعار | `app/Services/CountriesManagement/NotificationDefinitions/DeleteNotificationDefinition.php` |
| تكوين قنوات الإرسال (app/watsi/sms) | `app/Services/CountriesManagement/NotificationDefinitions/ConfigureNotificationChannels.php` |
| تعيين حالة قناة (forced/active/inactive) | `app/Services/CountriesManagement/NotificationDefinitions/SetNotificationChannelStatus.php` |

### Notifications (Instances) + Receivers

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض الإشعارات المرسلة/المجدولة | `app/Services/CountriesManagement/Notifications/ListNotifications.php` |
| إنشاء إشعار | `app/Services/CountriesManagement/Notifications/CreateNotification.php` |
| تحديث إشعار | `app/Services/CountriesManagement/Notifications/UpdateNotification.php` |
| حذف إشعار | `app/Services/CountriesManagement/Notifications/DeleteNotification.php` |
| عرض مستلمي الإشعار | `app/Services/CountriesManagement/NotificationReceivers/ListNotificationReceivers.php` |

---

## 6) Weekdays Settings

| عنوان الفنكشن | مكان الملف |
|---|---|
| عرض إعدادات أيام الأسبوع | `app/Services/CountriesManagement/WeekdaysSettings/ShowWeekdaysSettings.php` |
| تحديث إعدادات أيام الأسبوع | `app/Services/CountriesManagement/WeekdaysSettings/UpdateWeekdaysSettings.php` |

---

## 7) Entity Registration Customizations

| عنوان الفنكشن | مكان الملف |
|---|---|
| جلب إعدادات تخصيصات تسجيل الكيان (مع القيم الافتراضية) | `app/Services/CountriesManagement/EntityRegistrationCustomizations/GetSettings.php` |
| تحديث إعدادات إلزام الجوال/البريد | `app/Services/CountriesManagement/EntityRegistrationCustomizations/UpdateContactRequirements.php` |
| تفعيل/تعطيل نوع كيان أثناء التسجيل | `app/Services/CountriesManagement/EntityRegistrationCustomizations/UpdateEntityTypeStatus.php` |
| إضافة حقل مخصص | `app/Services/CountriesManagement/EntityRegistrationCustomizations/CreateCustomField.php` |
| تعديل حقل مخصص | `app/Services/CountriesManagement/EntityRegistrationCustomizations/UpdateCustomField.php` |
| حذف حقل مخصص | `app/Services/CountriesManagement/EntityRegistrationCustomizations/DeleteCustomField.php` |

> **ملاحظة**: `GetSettings.php` يحتوي على ثابت `ENTITY_TYPES` الذي يُعرّف أسماء أنواع الكيانات الثمانية بالترتيب، ويُستخدَم في المكوّن و Service آخر. كلا من `CreateCustomField` و `UpdateCustomField` يشتركان في منطق التحقق والبناء عبر methods عامة `validate()` و `build()`.
