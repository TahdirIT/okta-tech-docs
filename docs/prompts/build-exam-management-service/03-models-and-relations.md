العنوان: إنشاء الـ Eloquent Models والعلاقات الأساسية

المطلوب:
- أنشئ موديلات Eloquent لكل جداول الخدمة: ExamPeriod, ExamDay, ExamDayPeriod, Committee, CommitteeSeat, ExamSubject, ExamObserver, ExamAttendance.
- عرّف العلاقات بين الموديلات (hasMany, belongsTo, belongsToMany) بما يعكس:
  - فترة ← أيام ← فترات اليوم
  - لجنة ← مقاعد
  - فترات اليوم ← مواد/جلسات
  - مراقب ← جلسة (يوم+فترة+لجنة) عبر جدول ربط مناسب
  - حضور الطالب مرتبط بجلسة معيّنة وبطالب معيّن
- أضف Scopes مفيدة (مثل: activePeriod, forDay(date), forCommittee(…)).

مراجع داعمة للنمذجة:
- @okta-tech-docs/docs/services/exams-management/models/*
- @okta-tech-docs/docs/services/exams-management/overview.md

اعتبارات:
- استخدم أسماء حقول واضحة متطابقة مع الـ migrations.
- فعّل الحماية من التعبئة الشاملة/التبييض (fillable/guarded) حسب سياسة المشروع.

المخرجات:
- موديلات بالعلاقات والـ casts/attributes الضرورية وجاهزة للاستخدام في الخدمات. 

