# `entity_registration_customizations` (Country-level setting)

## الغرض

تخزين إعدادات **تخصيصات تسجيل الكيان** على مستوى الدولة، والتي تتحكم في:

- متطلبات بيانات التواصل الإلزامية أثناء التسجيل (جوال/بريد)
- ترتيب عرض **أنواع الكيانات** أثناء التسجيل
- تفعيل/تعطيل ظهور نوع كيان للمستخدم أثناء التسجيل
- تعريف **حقول مخصصة إضافية** تظهر حسب نوع الكيان، مع دعم:
  - عناوين متعددة اللغات (`label`)
  - خيارات متعددة اللغات للحقول الاختيارية (`options[].label`)
  - شروط الظهور (Conditional visibility)
  - إلزامية الإدخال عند الظهور

> المرجع الوظيفي/المنتجي: `docs/services/contries-management/guide/entity-registration-customizations.md`  
> المرجع UX: `docs/services/contries-management/user-experience/entity-registration-customizations-ux.md`

## أين تُخزّن؟

مثل بقية إعدادات الدولة، تُخزَّن داخل:

- جدول: `model_settings`
- العمود: `settings` (`jsonb`)
- على موديل الدولة: `model_type = App\Models\SupportedCountry`, `model_id = supported_countries.id`

> **ملاحظة**: المشروع لا يستخدم `morphMap`، لذلك `model_type` يكون اسم الكلاس الكامل.

ككائن (Object) تحت مفتاح:

- `settings.entity_registration_customizations`

## الشكل العام (Schema)

```json
{
  "contact_requirements": {
    "mobile_required": true,
    "email_required": false,
    "username_required": false,
    "national_id_required": false
  },
  "contact_validations": {
    "mobile": {
      "regex_rules": [
        {
          "regex": "/^05\\d{8}$/",
          "message": { "ar": "يجب أن يبدأ رقم الجوال بـ 05 ويتكوّن من 10 أرقام", "en": "Mobile must start with 05 and be 10 digits" }
        }
      ]
    },
    "national_id": {
      "regex_rules": [
        {
          "regex": "/^[12]\\d{9}$/",
          "message": { "ar": "رقم الهوية يجب أن يكون 10 أرقام ويبدأ بـ 1 أو 2", "en": "National ID must be 10 digits starting with 1 or 2" }
        }
      ]
    }
  },
  "entity_registration": {
    "types_order": [
      "individual_teacher",
      "administrative_school",
      "complex",
      "college",
      "university",
      "institute",
      "academy",
      "education_company"
    ],
    "types": {
      "individual_teacher": { "enabled": true },
      "administrative_school": { "enabled": true },
      "complex": { "enabled": true },
      "college": { "enabled": true },
      "university": { "enabled": true },
      "institute": { "enabled": true },
      "academy": { "enabled": true },
      "education_company": { "enabled": true }
    },
    "custom_fields": {
      "administrative_school": [
        {
          "type": "radio",
          "key": "school_gender",
          "label": { "ar": "نوع المدرسة", "en": "School type" },
          "options": [
            { "value": "boys", "label": { "ar": "بنين", "en": "Boys" } },
            { "value": "girls", "label": { "ar": "بنات", "en": "Girls" } },
            { "value": "mixed", "label": { "ar": "مختلطة", "en": "Mixed" } }
          ],
          "visibility": { "mode": "always" },
          "required_when_visible": true
        }
      ]
    }
  }
}
```

## التفاصيل

### 1) `contact_requirements`

- **`mobile_required`**: `boolean` — هل رقم الجوال إلزامي؟
- **`email_required`**: `boolean` — هل البريد الإلكتروني إلزامي؟
- **`username_required`**: `boolean` — هل اسم المستخدم إلزامي؟ (افتراضي: `false`)
- **`national_id_required`**: `boolean` — هل رقم الهوية الوطنية إلزامي؟ (افتراضي: `false`)

> يمكن أن يكون كلاهما إلزامي أو أحدهما أو كلاهما اختياري.

### 1.1) `contact_validations`

يُتيح تعريف قواعد تحقق (Regex) لحقلي الجوال ورقم الهوية:

- **`contact_validations.mobile.regex_rules`**: `array` — قواعد Regex للتحقق من رقم الجوال
- **`contact_validations.national_id.regex_rules`**: `array` — قواعد Regex للتحقق من رقم الهوية

كل قاعدة `regex_rules[i]` تحتوي على:
- **`regex`**: `string` — نمط PHP Regex (مثل: `/^05\d{8}$/`)
- **`message`**: `object` — رسالة خطأ متعددة اللغات:
  - `ar`: إلزامي
  - `en`: اختياري

> **ملاحظة**: مفتاح `contact_validations` يُخزَّن فقط عند وجود قواعد فعلية. إن كانت جميع القواعد فارغة فلا يُخزَّن في الـ JSON.

### 2) `entity_registration.types_order`

قائمة Strings تمثل ترتيب عرض أنواع الكيانات أثناء التسجيل.

- **ملاحظة**: القيم هنا تمثل **مفاتيح داخلية** (slugs)، بينما العناوين المعروضة للمستخدم يجب أن تطابق العناوين في `docs/tenants.md`.
- أسماء الأنواع الثمانية بالترتيب معرّفة في ثابت `ENTITY_TYPES` داخل `GetSettings.php`.

### 2.1) `entity_registration.types`

إعدادات لكل نوع كيان (اختياري)، أهمها:

- **`types.{entityType}.enabled`**: `boolean` — هل يظهر هذا النوع للمستخدم النهائي أثناء التسجيل؟

> في حال عدم وجود `types` أو عدم وجود كيان بعينه داخلها، يُعتبر **مفعّلًا افتراضيًا**.

### 3) `entity_registration.custom_fields`

كائن مفاتيحه هي **نوع الكيان** (مثل `administrative_school`) وقيمه مصفوفة من تعريفات الحقول.

#### 3.1) تعريف الحقل (Field definition)

- **`type`**: `string` — نوع الخانة، أحد:
  - `text`, `textarea`, `number`, `date`, `email`, `phone`, `url`
  - `select`, `multi_select`, `radio`, `checkbox`, `checkbox_group`
  - `file`
- **`key`**: `string` — مفتاح ثابت بصيغة `snake_case` (مثال: `license_number`)
- **`label`**: `object` — عناوين متعددة اللغات (مثال: `{ "ar": "...", "en": "..." }`)
- **`options`**: `array` — يظهر فقط للأنواع الاختيارية (`select/multi_select/radio/checkbox_group`)
  - `options[].value`: `string`
  - `options[].label`: `object` (i18n)
- **`visibility`**: `object`
  - `mode`: `always | conditional`
  - `when`: يظهر فقط عندما `mode = conditional` (انظر قسم الشروط)
- **`required_when_visible`**: `boolean`

#### 3.2) خصائص إضافية اختيارية (حسب النوع)

- **`accept`** (للملفات فقط): `array<string>` — امتدادات الملفات المسموح بها بدون نقاط (مثل: `["pdf","png","jpg"]`)
- **`validations`** (اختياري لأنواع متعددة): كائن يحتوي على:
  - **حدود الإدخال** (حسب النوع):
    - `text` / `textarea`: `min_length`, `max_length`
    - `number`: `min`, `max`
    - `date`: `min_date`, `max_date` (تنسيق `YYYY-MM-DD`)
    - `file`: `min_size_mb`, `max_size_mb`
    - `multi_select` / `checkbox_group`: `min_selected`, `max_selected`
  - **`regex_rules`** (لأنواع: `text`, `textarea`, `number`, `email`, `phone`, `url`):
    - `array` من القواعد، كل قاعدة:
      - `regex`: `string` — نمط PHP Regex
      - `message`: `object` — رسالة خطأ (`ar` إلزامي، `en` اختياري)

> **ملاحظة**: مفتاح `validations` يُخزَّن فقط عند وجود قيم فعلية.

## شروط الظهور (Conditional visibility)

عند `visibility.mode = conditional` يكون `visibility.when` على الشكل:

```json
{ "field": "school_gender", "operator": "equals", "value": "girls" }
```

الحقول:

- **`field`**: `string` — مفتاح الحقل المرجعي الذي يعتمد عليه شرط الظهور
- **`operator`**: `string` — أحد:
  - `equals`, `not_equals`
  - `in`, `not_in`
  - `is_true`, `is_false`
  - `exists`
- **`value`**: `any` — قيمة/قيم الشرط (قد تكون `string | number | boolean | array`)

> **ملاحظة**: قيمة `value` تُتجاهَل عند استخدام `is_true`, `is_false`, `exists`.

## القيود والتحقق (Validation / Constraints)

- **`key`**:
  - صيغة `snake_case` (يسمح بـ `a-z`, `0-9`, `_`)
  - **فريد** ضمن (الدولة + نوع الكيان)
  - يُفضّل عدم تغييره بعد الاستخدام لتجنب كسر البيانات التاريخية
- **`options`**:
  - إلزامية للأنواع الاختيارية (`select`, `multi_select`, `radio`, `checkbox_group`)
  - كل `value` داخل `options` يجب أن يكون فريدًا ضمن الحقل
- **`visibility.when`**:
  - إلزامي عند الوضع المشروط
  - يجب ألّا يشير الحقل إلى نفسه (منع حلقات الاعتماد الذاتي)
- **اللغات**:
  - `label.ar` إلزامي، `label.en` اختياري
