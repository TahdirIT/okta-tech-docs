# CLAUDE.md

هذا الملف يوجّه Claude Code (وأي مساعد ذكاء اصطناعي آخر مثل Cursor) عند العمل داخل هذا المشروع.

## نظرة عامة

**okta-tech-docs** هو المرجع الرسمي للتوثيق التقني والمعايير الهندسية لمنصة **أوكتا التعليمية**. المحتوى الأساسي مكتوب بالعربية ويصف:

- **الرؤية والخدمات الأساسية** للمنصة.
- **الفئات المستهدفة** (المعلم الفردي، المدرسة، المجمع، الكلية، الجامعة، المعهد، الأكاديمية، الشركة التعليمية).
- **منصة الشركاء** (Partner Platform) وآلية التكامل عبر APIs.
- **المعايير التقنية** (Tech Standards) التي تلتزم بها المشاريع الأخرى: `okta-web` و `okta-partners`.

هذا repo للتوثيق فقط — **لا يحتوي كود تطبيقي**.

## بنية المجلدات

```
docs/
├── README.md                       # نظرة عامة على المنصة
├── end-users.md                    # المستخدمون النهائيون
├── packages.md                     # حزم/اشتراكات الخدمات
├── partner-platform.md             # رؤية منصة الشركاء
├── tenants.md                      # أنواع الكيانات التعليمية
├── translations.md
├── pages/                          # صفحات إضافية
├── prompts/                        # prompts جاهزة لمساعدات الـ AI
├── services/                       # توثيق الخدمات التفصيلي
└── tech-standards/                 # المعايير الهندسية (المرجع لكل repos)
    ├── README.md
    ├── design-standards.md
    ├── permissions-naming.md
    └── laravel-feature-services-structure.md
tmp/                                # ملفات مؤقتة (لا تُعتمد كمرجع)
```

## المعايير الحالية المُعتمدة

### `tech-standards/laravel-feature-services-structure.md`
- `app/Services/<Feature>/<Resource>/<Function>.php`
- كل Use-case كلاس واحدة مع `__invoke()`، بدون `XxxService.php` عامة.

### `tech-standards/permissions-naming.md`
- الصيغة: `<feature>.<resource>.<action>` — **lowercase** + **dot-separated** + **snake_case** داخل الجزء.
- أفعال محددة (`view`, `create`, `update`, `delete`, `activate`)، لا wildcards.

### `tech-standards/design-standards.md`
- معايير الهوية البصرية والتصميم للمنصة.

## إرشادات التحرير (مهمة)

- **اللغة**: المحتوى الأساسي **بالعربية**. حافظ على الأسلوب والمصطلحات المستخدمة حالياً (مثل: «الفئة المستهدفة»، «الصلاحيات»، «الكيانات التعليمية»). إن أُضيف محتوى إنجليزي، اجعله ترجمة موازية ومنسَّقة وليس بديلاً.
- **RTL**: احرص على تنسيق Markdown يعمل مع العرض RTL (مسافات قبل الرموز، استخدام `-` للقوائم، عدم خلط اتجاهات داخل السطر دون فاصل).
- **الروابط الداخلية**: استخدم مسارات نسبية (مثل `./permissions-naming.md`) وتحقق أنها تعمل.
- **الـ Code blocks**: اكتب الأمثلة البرمجية بالإنجليزية كما هي معتادة (PHP/Laravel). لا تُعرِّب أسماء classes أو namespaces.
- **الفهرس**: عند إضافة ملف جديد في `tech-standards/`، حدِّث `tech-standards/README.md`. عند إضافة ملف جديد في `docs/`، أضف إشارة إليه من `docs/README.md` عند الاقتضاء.
- **الأمثلة الصحيحة/الخاطئة**: أضف أمثلة واضحة (✅/❌) عند توثيق معيار جديد — كما في `permissions-naming.md`.
- **تحديث المعايير**: أي تغيير في معيار قائم **قد يكسر** `okta-web` و `okta-partners`. أشِر بوضوح إلى أن التغيير breaking ووضّح خطة الترحيل.
- **مجلد `tmp/`**: مخصص لمسودات/ملفات مؤقتة — لا تعتمده مرجعاً، ولا تربط إليه من ملفات موثّقة.
- **لا تُنشئ ملفات توثيق في جذر الـ repo** — ضعها داخل `docs/` أو مجلد فرعي مناسب.

## المشاريع المرتبطة (المستهلِكة لهذه المعايير)

- [`tahdirit/okta-web`](https://github.com/tahdirit/okta-web) — التطبيق الأساسي (Laravel 12 + Livewire 4 + nwidart/laravel-modules).
- [`tahdirit/okta-partners`](https://github.com/tahdirit/okta-partners) — منصة الشركاء و الـ APIs (Laravel 13 + Livewire 4 + JWT).

عند تعديل معيار هنا، يجب التحقق من أن CLAUDE.md في هذه المشاريع لا يزال يتوافق مع التغيير.

## أدوات مفيدة

- Markdown preview في المحرر للتحقق من الهيئة قبل commit.
- فحص الروابط الميتة: `markdown-link-check docs/**/*.md` (اختياري).
