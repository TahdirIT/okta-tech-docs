العنوان: تنظيم Use-cases داخل Services وفق معيار Feature Services Structure

المطلوب:
- نظّم الخدمات داخل مساحة `Services` بالـ Module باتباع معيار @okta-tech-docs/docs/tech-standards/laravel-feature-services-structure.md:
  - ExamsManagement/<Resource>/<UseCase>.php
- قسّم الموارد بحسب نطاقات الخدمة:
  - Periods, Days, DayPeriods, Committees, CommitteeSeats, Subjects, Observers, Attendance, Reports
- أنشئ ملفات Use-cases صغيرة بمسؤولية واحدة مثل:
  - Periods/ListPeriods.php, Periods/CreatePeriod.php, Periods/ConfirmPeriod.php, Periods/ReplicatePeriod.php
  - Committees/CreateCommittee.php, Committees/ConfigureSeats.php
  - Observers/AssignObserver.php
  - Attendance/RecordAttendance.php, Attendance/MarkAllPresent.php
- استخدم `__invoke()` وتبنَّي حقن الاعتمادية عبر الـ constructor.

اعتبارات:
- لا تضع منطق HTTP داخل الخدمات.
- وفّر توقيعات دوال واضحة ومدخلات/مخرجات صريحة (فكّر في DTO لو لزم).

مراجع:
- حالات/تدفّقات العمل: @okta-tech-docs/docs/services/exams-management/user-flows/*

المخرجات:
- شجرة Services تحتوي موارد واضحة وUse-cases لكل عملية رئيسية. 

