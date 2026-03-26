# إنشاء خدمتي Tenant Registration + User Management في `okta-web` (Prompt جاهز لـ Claude)

هذا الملف عبارة عن **Prompt كامل جاهز للنسخ** إلى Claude لتنفيذ خدمتي:

- `docs/services/tenant-registration`
- `docs/services/user-management`

داخل مشروع Laravel: `okta-web` مع الالتزام بما هو مطبق فعلاً في المشروع وبمعايير `docs/tech-standards`.

---

## السياق والمراجع التي يجب على Claude قراءتها أولًا

- `docs/tech-standards/laravel-feature-services-structure.md`
- `docs/tech-standards/permissions-naming.md`
- `docs/tech-standards/design-standards.md`
- `docs/services/tenant-registration/guide/README.md`
- `docs/services/tenant-registration/tech/service_functions.md`
- `docs/services/tenant-registration/tech/models/README.md`
- `docs/services/user-management/README.md`
- `docs/services/user-management/tech/service_functions.md`
- `docs/services/user-management/tech/models/README.md`

---

## حقائق مهمة عن `okta-web` (لا تفترض غيرها)

هذه الحقائق يجب اعتبارها “مصدر الحقيقة” أثناء التنفيذ:

- المشروع Laravel 12 + Livewire 4 + Fortify 1 + Pest.
- جداول المستخدمين لا تحتوي `email/password`:
  - جدول `users` يحتوي: `name`, `status`, `default_country_id`, `last_login_at` … (بدون `email/password`).
  - بيانات الدخول تعتمد على:
    - `user_identifiers` (`type`, `value`, `country_id`, `verified_at`, `is_primary`)
    - `user_credentials` (`password_hash`)
- تسجيل الدخول الحالي موجود عبر Livewire: `resources/views/pages/auth/login/login.php`.
- الـ RBAC موجود (Spatie Permission) لكن **التحقق المستخدم في التطبيق** يتم عبر:
  - Middleware: `app/Http/Middleware/CheckPermission.php` يقرأ `session('context.permission_names')`
  - بناء السياق: `app/Services/ContextBuilder.php`
  - API سياق: `routes/api.php` + Controllers داخل `app/Http/Controllers/Api/*`
- يوجد خدمات “قديمة” داخل `app/Services/*.php`، لكن معيارنا المطلوب للميزات الجديدة هو:
  - `app/Services/<Feature>/<Resource>/<Function>.php` مع `__invoke()`

---

## Prompt (جاهز لـ Claude)

```text
أنت تعمل الآن على مشروع Laravel اسمه okta-web. المطلوب: تنفيذ خدمتي tenant-registration و user-management حسب توثيق okta-tech-docs، مع الالتزام بما هو مطبق فعلاً داخل okta-web.

### 0) قواعد عامة (مهمة جدًا)
- لا تغيّر أي dependency.
- التزم بمعيار Feature Services:
  app/Services/<Feature>/<Resource>/<Function>.php
  وكل Use-case عبارة عن Class واحدة و __invoke().
- لا تفترض وجود حقول في DB غير موجودة فعلاً. افحص migrations الحالية قبل أي إضافة.
- نفّذ أقل نطاق ممكن لتحقيق use-cases المطلوبة. أي جدول “اختياري/مقترح” في التوثيق لا يُنفّذ إلا إذا كان ضروريًا ومبررًا.
- بعد التنفيذ: اكتب/حدّث اختبارات Pest المناسبة، وشغّل أقل مجموعة اختبارات مرتبطة.

### 1) افحص ما هو موجود فعليًا قبل البدء
اقرأ سريعًا هذه الملفات داخل okta-web لتبنّي نفس الأنماط:
- app/Models/User.php
- app/Models/UserIdentifier.php
- app/Models/UserCredential.php
- app/Models/Tenant.php
- database/migrations/*_create_users_table.php
- database/migrations/*_create_user_identifiers_table.php
- database/migrations/*_create_user_credentials_table.php
- database/migrations/*_create_tenants_table.php
- database/migrations/*_create_tenant_user_table.php
- resources/views/pages/auth/login/login.php
- app/Services/ContextBuilder.php
- app/Http/Middleware/CheckPermission.php
- routes/api.php و routes/web.php

### 2) تنفيذ Feature: User Management
طبّق use-cases الأساسية حسب:
docs/services/user-management/tech/service_functions.md

أنشئ ملفات (على الأقل) ضمن:
- app/Services/UserManagement/Users/RegisterUser.php
- app/Services/UserManagement/Auth/LoginUser.php (إن احتجنا فصل منطق Livewire)
- app/Services/UserManagement/Users/UpdateUserProfile.php (إن كان مطلوبًا)
- app/Services/UserManagement/Identifiers/UpsertUserIdentifier.php
- app/Services/UserManagement/Credentials/UpdateUserPassword.php

سلوك RegisterUser (مهم):
- لا تستخدم users.email أو users.password لأنها غير موجودة.
- أنشئ User + UserCredential(password_hash) + UserIdentifier حسب payload.
- طبّق uniqueness حسب user_identifiers unique(type,value,country_id).
- استخدم سياسة كلمات المرور الحالية (PasswordValidationRules أو ما يعادلها).

ملاحظة مهمة:
- Fortify registration الحالية تعتمد على CreateNewUser وتفترض email/password؛ هذا غير متوافق مع schema الحالي.
  عدّل مسار التسجيل بحيث يصبح متوافقًا مع user_identifiers/user_credentials (إما عبر تعديل Action أو إلغاء screen إن لم يكن مستخدمًا)، مع الحفاظ على اختبارات التسجيل أو تحديثها لتعكس السلوك الصحيح.

### 3) تنفيذ Feature: Tenant Registration
طبّق use-cases حسب:
docs/services/tenant-registration/tech/service_functions.md

المطلوب (حد أدنى):
- app/Services/TenantRegistration/Customization/GetEntityRegistrationCustomization.php
  - يعيد متطلبات الحقول + الأنواع المفعّلة + schema للحقول المخصصة حسب الدولة (إن كانت موجودة فعليًا في okta-web؛ وإلا أعد هيكلًا واضحًا مع TODOs وعدم كسر الواجهة).
- app/Services/TenantRegistration/Tenants/RegisterTenant.php
  - ينشئ Tenant + يربط Owner user عبر tenant_user
  - يدعم مسارين:
    - مستخدم جديد (ينادي RegisterUser من UserManagement)
    - مستخدم موجود (Login ثم ربطه كـ Owner)
  - لا تنشئ tenant_registration_sessions إلا إذا احتجنا “استئناف” فعلاً.

### 4) RBAC + Permissions
- عند إضافة أي صلاحيات جديدة اتبع معيار:
  <feature>.<resource>.<action> (lowercase + snake_case داخل الجزء)
  راجع docs/tech-standards/permissions-naming.md
- انتبه: التحقق داخل التطبيق يتم عبر session context.permission_names.
  أي صفحات/أجزاء UI محمية يجب أن تستخدم نفس آلية الصلاحيات الحالية (Middleware CheckPermission أو @can مع ربطها بسياق الجلسة حسب الموجود).

### 5) UI/UX (إن تطلّب tenant-registration واجهة)
التوثيق يقترح أن تدفق “تسجيل كيان جديد” يكون ضمن:
- Landing Page
- Login Page (Wizard)

في okta-web يوجد LandingPage route و Livewire login page.
نفّذ أقل تغيير: أضف خيار/زر واضح في landing أو login يفتح Wizard داخل صفحة login (مثلاً tab/stepper).
التزم بمعايير التصميم واللغة (RTL/EN) في docs/tech-standards/design-standards.md.

### 6) الاختبارات
- أضف/حدّث اختبارات Pest لسيناريوهات:
  - RegisterUser ينشئ user + identifier + credential بشكل صحيح + يمنع التكرار.
  - RegisterTenant ينشئ tenant ويربط owner في tenant_user.
  - تحديث تسجيل Fortify/Registration لا يكسر الاختبارات أو عدّل الاختبارات بما يعكس الواقع.

### 7) مخرجات مطلوبة في النهاية
- قائمة الملفات التي تم إنشاؤها/تعديلها.
- شرح موجز لكيفية تشغيل الاختبارات التي أضفتها.
```

