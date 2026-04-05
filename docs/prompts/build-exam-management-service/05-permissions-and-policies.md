العنوان: تصميم الصلاحيات (Permissions) والسياسات (Policies)

المطلوب:
- عرّف أكواد الصلاحيات وفق معيار @okta-tech-docs/docs/tech-standards/permissions-naming.md بصيغة: `exams_management.<resource>.<action>`.
- أمثلة مطلوبة:
  - `exams_management.periods.view|create|update|confirm|replicate`
  - `exams_management.committees.view|create|update`
  - `exams_management.observers.assign`
  - `exams_management.attendance.record|mark_all_present`
  - `exams_management.reports.view|print`
- أنشئ Policies تغطي الموارد الأساسية، واربطها بالـ Controllers.
- احترم الأدوار المذكورة في @okta-tech-docs/docs/services/exams-management/overview.md (منسق/مراقب/طالب) وقيّد الوصول تبعاً لذلك.

اعتبارات:
- لا تستخدم wildcards.
- اختبر الصلاحيات عبر Middleware/Policy على كل Route حساس.

المخرجات:
- تعريف الصلاحيات + Policies مفعّلة ومستخدمة في طبقة HTTP. 

