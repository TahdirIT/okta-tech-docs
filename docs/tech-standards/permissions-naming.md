# معيار تسمية أكواد الصلاحيات (Permissions Naming Standard)

## الهدف

توحيد طريقة تسمية الصلاحيات بحيث تكون:

- **ثابتة (Deterministic)** ولا تعتمد على اجتهادات
- **قابلة للقراءة** للبشر
- **قابلة للتحقق** آلياً عند التسجيل/النشر

---

## الصيغة المعتمدة

الصيغة العامة:

`<feature>.<resource>.<action>`

قواعد الصياغة:

- **Lowercase فقط**
- **Dot-separated** للفصل بين الأجزاء الرئيسية (`feature`, `resource`, `action`)
- داخل الجزء الواحد (خصوصاً `resource`) استخدم **snake_case** للأسماء المركبة

---

## متى نستخدم `snake_case`؟

عند وجود كلمات متعددة داخل نفس الجزء:

- ✅ `academic_years`
- ✅ `country_data`
- ✅ `weekdays_settings`

> ملاحظة: هذا متوافق مع أنماط شائعة في الكود مثل استخدام `Str::snake()` لتوليد أسماء الموارد.

---

## أمثلة صحيحة / خاطئة

### مثال: إدارة الدول

- ✅ `countries_management.academic_years.terms.set_active`
- ✅ `countries_management.weekdays_settings.update`

### أمثلة خاطئة (مرفوضة)

- ❌ `countries_management.weekdays-settings.update`  
  السبب: استخدام `-` داخل `resource` غير متوافق مع معيار **dot-separated + lowercase** ولا مع نمط `snake_case`.

- ❌ `CountriesManagement.weekdays_settings.update`  
  السبب: يجب أن تكون **lowercase بالكامل**.

- ❌ `countries_management.weekdays_settings.*`  
  السبب: **Wildcards غير مسموحة**.

---

## توصيات للأفعال (Actions)

استخدم أفعال دقيقة قدر الإمكان مثل:

- `view`
- `create`
- `update`
- `delete`
- `activate`

وتجنب الأفعال العامة مثل `manage` إلا عند وجود معنى محدد ومتفق عليه.

