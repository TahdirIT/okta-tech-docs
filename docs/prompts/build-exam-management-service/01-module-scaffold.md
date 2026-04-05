العنوان: إنشاء Module لخدمة إدارة الاختبارات داخل مشروع @okta-web

المطلوب:
- أنشئ Module باسم ExamsManagement داخل مشروع Laravel @okta-web وفق تنظيم Modules المتبع في المشروع.
- جهّز هيكل المجلدات الأساسي داخل الـ Module بحيث يدعم طبقات: Http (Controllers, Requests, Resources), Services, Policies, Models, Database (migrations, seeders, factories), Routes, Views (Blade) إن لزم.
- اربط الـ Module بآلية التحميل والتسجيل في التطبيق (ServiceProvider داخل الـ Module) مع مساحات الأسماء الصحيحة.
- أضف RouteServiceProvider خاص بالـ Module وتحميل ملفات الراوت الخاصة به (api.php, web.php) إن وُجدت.

اعتبارات ومعايير:
- راجع @okta-tech-docs/docs/tech-standards/laravel-feature-services-structure.md لتقسيم الخدمات داخل `app/Services` أو داخل مساحة Services في الـ Module بنفس المعيار.
- احترم معايير التسمية والهيكلة المذكورة في ملفات @okta-tech-docs/docs/tech-standards/*.
- اجعل الـ Module قابلاً للتوسّع بدون تداخل مع أجزاء أخرى من المنصة.

مراجع:
- نطاق الخدمة ونمذجتها على مستوى المفاهيم: @okta-tech-docs/docs/services/exams-management/overview.md
- تدفقات المستخدم والأدوار: @okta-tech-docs/docs/services/exams-management/user-flows/* و user-journeys/*

المخرجات:
- شجرة مجلدات Module جاهزة.
- ServiceProvider + RouteServiceProvider مفعّلان.
- توثيق موجز في README داخل الـ Module يوضح الغرض والبنية. 

