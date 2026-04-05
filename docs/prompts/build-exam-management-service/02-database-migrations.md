العنوان: تصميم مخطط قاعدة البيانات (Migrations) لخدمة إدارة الاختبارات

المطلوب:
- صمّم وأنشئ Migrations تغطي الكيانات المفاهيمية التالية وفق @okta-tech-docs/docs/services/exams-management/overview.md:
  - exam_periods, exam_days, exam_day_periods (الفترات الزمنية داخل اليوم)
  - committees (اللجان/القاعات) مع دعم الأعمدة/الصفوف وتخصيص المقاعد (committee_seats)
  - exam_subjects وربطها بـ exam_day_periods
  - exam_observers (إسناد معلم كمراقب) وربطه بجلسة (يوم+فترة+لجنة)
  - exam_attendance لتسجيل حضور الطالب في جلسة محددة
- ضَع قيود التكامل (FKs, unique constraints) لمنع التعارضات المذكورة في القسم "ضمان الاتساق والجودة" في الـ overview.
- احترم سياسة "فترة واحدة فعّالة" عبر حقل state/status + فهرس/قيد مناسب أو منطق على مستوى التطبيق لاحقاً.

اعتبارات:
- أعمدة قياسية (id, created_at, updated_at).
- فهارس لأعمدة الربط المتكررة للوصول السريع (performance).
- تحضير جداول pivot/ربط عند الحاجة (مثل ربط الطلاب بالمقاعد/اللجان/الجلسات).

مراجع:
- @okta-tech-docs/docs/services/exams-management/overview.md

المخرجات:
- جميع ملفات الـ migrations مع أسماء مرتبة وواضحة.
- لا تستخدم أعمدة عامة غير مُسماة بوضوح. 

