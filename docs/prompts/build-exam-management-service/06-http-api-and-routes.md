العنوان: تصميم طبقة HTTP (Routes, Controllers, Requests, Resources)

المطلوب:
- أنشئ مسارات REST/Action-based لموارد الخدمة داخل ملفي web.php و api.php في Module ExamsManagement.
- أنشئ Controllers صغيرة لكل مورد، تربط كل أكشن بـ Use-case مناسب في Services.
- عرّف FormRequest للتحقق من المدخلات، وResource/ResourceCollection للاستجابات.
- نقاط نهاية أساسية:
  - فترات: list/show/create/update/confirm/replicate
  - اللجان: list/create/update/configure-seats
  - الأيام/فترات اليوم: list/create/update
  - المراقبون: assign/list
  - الحضور: record/mark-all-present
  - التقارير: list/print

اعتبارات:
- ربط Middleware للأذونات Policies/Permissions.
- توحيد رسائل الأخطاء وحالات النجاح وفق @okta-tech-docs/docs/services/exams-management/overview.md (حالات الواجهة).

المخرجات:
- Routes+Controllers+Requests+Resources مترابطة وجاهزة للاستهلاك من الواجهات. 

