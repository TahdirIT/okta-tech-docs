# مقترحات الفصل المنطقي بين الخدمات (Service Separation Recommendations)

## نظرة عامة

هذا المستند يقدم مقترحات لتحسين الفصل المنطقي بين الخدمات باعتبار أن كل service يمثل Module أو Microservice مستقل.

---

## 1. مبادئ الفصل المنطقي الأساسية

### 1.1 Business Capability Boundary (حدود القدرة التجارية)
**المبدأ:** كل خدمة يجب أن تمثل قدرة تجارية متماسكة وقابلة للفهم بشكل مستقل.

✅ **مثال جيد:**
- `attendance-management`: قدرة تجارية واضحة (إدارة الحضور والغياب)
- `subscription-billing`: قدرة تجارية متماسكة (إدارة الاشتراكات والفوترة)

❌ **مثال سيء:**
- خدمة تدمج "إدارة الطلاب" و"إدارة الفوترة" (قدرتان تجاريتان مختلفتان)

---

### 1.2 Data Ownership (ملكية البيانات)
**المبدأ:** كل خدمة تملك بياناتها بشكل كامل ومستقل.

✅ **التطبيق الحالي:**
- Database per Service pattern
- External Data Dependencies كقراءة فقط
- لا توجد JOINs عبر الخدمات

⚠️ **نقطة مهمة:**
- عند الحاجة لبيانات من خدمة أخرى، استخدم:
  - **Domain Events** للتفاعل غير المتزامن
  - **API calls** للتفاعل المتزامن
  - **Data Replication/Cache** للقراءة المتكررة

---

### 1.3 Behavior Encapsulation (تغليف السلوك)
**المبدأ:** السلوك (Business Logic) يحدد حدود الخدمة، وليس البيانات فقط.

✅ **أمثلة:**
- `attendance-management` → سلوك: تسجيل الحضور، التحقق من الغياب، حساب الإحصائيات
- `employee-management` → سلوك: إدارة الموظفين، تعيين الأدوار، دورة الحياة

---

## 2. تقييم الفصل الحالي

### 2.1 Kernel Services (الخدمات الأساسية) ✅

الخدمات الحالية في `kernel/` تمثل قدرات متعددة الاستخدامات:

| الخدمة | التقييم | ملاحظات |
|--------|---------|---------|
| `authentication-authorization` | ✅ جيد | قدرة واضحة ومستقلة |
| `user-management` | ✅ جيد | إدارة الهويات والبيانات الأساسية |
| `roles-permissions` | ✅ جيد | نظام الصلاحيات المركزي |
| `subscription-billing` | ✅ جيد | إدارة الاشتراكات والمدفوعات |
| `location` | ⚠️ محتمل | قد تكون Reference Data فقط |
| `messaging` | ✅ جيد | قدرة اتصال مستقلة |
| `notifications` | ✅ جيد | قدرة إشعارات مستقلة |
| `file-management` | ✅ جيد | إدارة الملفات |
| `settings` | ⚠️ غامض | يحتاج توضيح: ما هو "settings"؟ |

**مقترحات:**

1. **Location Service:**
   - إذا كانت Reference Data فقط (Country, City, Region) → قد تكون جزء من Kernel Config
   - إذا كان هناك سلوك معقد (تحديد الموقع، التحقق الجغرافي) → خدمة مستقلة ✅

2. **Settings Service:**
   - يحتاج توضيح: هل هي Feature Flags؟ Configuration؟ System Settings؟
   - اقتراح: إذا كانت Feature Flags → `feature-flags` أو `configuration`
   - إذا كانت System Settings → قد تندمج مع Kernel Config

---

### 2.2 Domain Services (الخدمات المجالية) ✅

الخدمات الحالية في `domain/` تمثل قدرات مجالية مخصصة:

#### ✅ خدمات جيدة ومتماسكة:

| الخدمة | التقييم | السبب |
|--------|---------|-------|
| `attendance-management` | ✅ ممتاز | قدرة تجارية واضحة ومستقلة |
| `employee-management` | ✅ جيد | إدارة الموظفين ككيان مستقل |
| `student-management` | ✅ جيد | إدارة الطلاب ككيان مستقل |
| `school-management` | ✅ جيد | إدارة المدارس والمجمعات |
| `exam-management` | ✅ جيد | عملية امتحانات متماسكة |
| `timetable-management` | ✅ جيد | إدارة الجداول الزمنية |
| `subject-grade-management` | ✅ جيد | إدارة المواد والدرجات |
| `subscription-billing` | ✅ جيد | في kernel (صحيح) |

#### ⚠️ خدمات تحتاج مراجعة:

| الخدمة | المشكلة المحتملة | المقترح |
|--------|------------------|---------|
| `calls-management` | قد يكون مرتبط بـ `attendance-management` | إذا كان Call جزء من Attendance → دمج، وإلا → مستقل ✅ |
| `dismissal-management` | قد يكون مرتبط بـ `attendance-management` | نفس المنطق: هل Dismissal = نوع Attendance؟ |
| `excuse-management` | قد يكون مرتبط بـ `attendance-management` | هل Excuse = نوع Attendance أو عملية منفصلة؟ |
| `class-operations` | علاقات معقدة مع خدمات أخرى | إذا كانت Operation = Attendance في الصف → قد يكون جزء من `attendance-management` |
| `reports-analytics` | قدرة عامة قد تكون Infrastructure | هل هي خدمة مجالية أم قدرة بنية تحتية؟ |

---

## 3. مقترحات التحسين

### 3.1 دمج الخدمات ذات العلاقة الوثيقة

#### المقترح الأول: Attendance Domain Consolidation

**الخدمات المرشحة للدمج:**
- `attendance-management` (الأساسي)
- `dismissal-management` (نوع من الحضور/الغياب)
- `excuse-management` (متعلق بالغياب)
- `class-operations` (إذا كانت مرتبطة بالحضور في الصف)

**الخدمة المقترحة:** `attendance-management`

**المبررات:**
- جميعها تدور حول "تتبع الحضور والغياب"
- علاقات وثيقة بينها (Dismissal يؤثر على Attendance)
- قواعد عمل مشتركة (التحقق من التواريخ، الحسابات)
- تقليل التعقيد في التكامل

**البديل:** إذا كانت Dismissal و Excuse عمليات مستقلة معقدة → ابقاءها منفصلة ✅

---

#### المقترح الثاني: Review Reports-Analytics

**الخدمة الحالية:** `reports-analytics`

**الأسئلة:**
1. هل تقوم بـ "إنشاء تقارير" كعملية تجارية؟
2. أم هي "بنية تحتية للتحليلات"؟

**السيناريوهات:**

**سيناريو 1: Reporting as Infrastructure**
- إذا كانت توفر أدوات عامة للتقارير لجميع الخدمات
- المقترح: نقلها إلى `kernel/reporting` أو `kernel/analytics`
- دورها: قدرة مساعدة عامة

**سيناريو 2: Domain-Specific Reports**
- إذا كانت تقوم بعمليات تقارير خاصة بالمجال التعليمي
- المقترح: ابقاءها في `domain/reports-analytics` ✅
- دورها: قدرة تجارية محددة

**الخلاصة:** اعتمادًا على محتوى `process.md` و `tool-link.md` → قد تكون Infrastructure

---

### 3.2 تحسين الحدود (Boundaries)

#### أ. توثيق External Data Dependencies

**الحالة الحالية:** ✅ جيدة (موثقة في `employee.md`)

**المقترحات:**
- توحيد نمط التوثيق في جميع الخدمات
- إضافة `Access Patterns` بوضوح (read-only, async events, etc.)
- توثيق `Data Contracts` بين الخدمات

---

#### ب. توثيق Domain Events

**الحالة الحالية:** ملفات `domain-events.md` موجودة لكن فارغة

**المقترحات:**
- توثيق جميع Domain Events لكل خدمة
- تحديد Producers و Consumers المحتملين
- مثال:

```markdown
## Domain Events

### AttendanceMarked
- Emitted by: attendance-management
- Payload: { employee_id, date, status, school_id }
- Potential Consumers:
  - reports-analytics (للإحصائيات)
  - notifications (لإشعارات الغياب)
```

---

#### ج. توثيق Service Boundaries

**الحالة الحالية:** ملفات `boundaries.md` فارغة

**المقترحات:**
- تعريف واضح لما "داخل" و "خارج" كل خدمة
- تحديد APIs (Public vs Internal)
- مثال:

```markdown
## Service Boundaries

### Inside the Boundary (Owned)
- Employee model and lifecycle
- Employee-School assignments
- Employee role assignments per school

### Outside the Boundary (Dependencies)
- User data (from user-management) - read-only
- Role definitions (from roles-permissions) - read-only
- School data (from school-management) - read-only

### Public API
- createEmployee()
- assignEmployeeToSchool()
- getEmployeeRoles()

### Internal (Not exposed)
- Employee soft-delete logic
- Internal role validation
```

---

### 3.3 تحسين التسميات والتصنيفات

#### أ. توحيد أسماء الخدمات

**النمط الحالي:** `kebab-case` (مثال: `employee-management`)

**المقترحات:**
- استخدام نمط موحد في جميع الخدمات ✅
- تجنب الاختصارات غير الواضحة
- استخدام أسماء تصف "القدرة" وليس "الكيان"

**أمثلة:**
- ✅ `employee-management` (القدرة: إدارة الموظفين)
- ✅ `attendance-management` (القدرة: إدارة الحضور)
- ⚠️ `reports-analytics` (قد يكون `reporting` أو `analytics` فقط)

---

#### ب. تصنيف الخدمات بشكل واضح

**البنية الحالية:**
```
services/
  kernel/          # خدمات أساسية متعددة الاستخدامات
  domain/          # خدمات مجالية مخصصة
```

**المقترح:** إضافة تصنيفات فرعية:

```
services/
  kernel/
    identity/      # الهوية والمصادقة
      - authentication-authorization
      - user-management
    access-control/ # التحكم في الوصول
      - roles-permissions
    commerce/      # التجارة والمدفوعات
      - subscription-billing
    infrastructure/ # البنية التحتية
      - file-management
      - location (إذا كانت reference data)
      - notifications
      - messaging
      - settings
  domain/
    academic/      # العمليات الأكاديمية
      - exam-management
      - subject-grade-management
      - timetable-management
    operations/    # العمليات اليومية
      - attendance-management
      - class-operations
    people/        # إدارة الأشخاص
      - employee-management
      - student-management
      - guardian-management
    administration/ # الإدارة
      - school-management
      - conduct-discipline
```

**ملاحظة:** هذا التصنيف اختياري وقد يضيف تعقيدًا. البنية الحالية (`kernel/domain/`) كافية ✅

---

## 4. معايير تقييم الفصل المنطقي

### 4.1 Checklist لخدمة جيدة

- [ ] **Capability Coherence:** هل الخدمة تمثل قدرة تجارية واحدة متماسكة؟
- [ ] **Data Ownership:** هل البيانات مملوكة بشكل كامل للخدمة؟
- [ ] **Behavior Independence:** هل السلوك مستقل بدرجة كبيرة؟
- [ ] **Clear Dependencies:** هل التبعيات موثقة وواضحة؟
- [ ] **Event-Driven Ready:** هل يمكن التفاعل عبر Events؟
- [ ] **Extractability:** هل يمكن استخراجها كـ Microservice مستقلة؟

---

### 4.2 Red Flags (علامات الخطر)

⚠️ **تحذيرات تشير إلى فصل منطقي ضعيف:**

1. **خدمتان تصلان لنفس البيانات مباشرة:**
   - مثال: `attendance-management` و `reports-analytics` يصلان لجدول `attendances`
   - الحل: أحداهما يملك البيانات، الآخر يستخدم API/Events

2. **خدمتان تعتمدان على بعضهما بشكل متزامن:**
   - مثال: `employee-management` يعتمد على `school-management` والعكس
   - الحل: إعادة تصميم أو دمج إذا كانت متلازمة

3. **خدمة تملك بيانات لكن لا توجد لها عملية تجارية:**
   - مثال: خدمة `location` تحتوي على Country, City فقط (Reference Data)
   - الحل: دمجها مع Kernel Config أو Service آخر

4. **قواعد عمل موزعة عبر خدمات متعددة:**
   - مثال: قواعد Attendance موزعة على 3 خدمات
   - الحل: دمج الخدمات أو توحيد القواعد في خدمة واحدة

---

## 5. خطة التنفيذ المقترحة

### المرحلة 1: التحليل والتوثيق (الأولوية: عالية)

1. **ملء ملفات `boundaries.md`:**
   - تعريف واضح لحدود كل خدمة
   - تحديد APIs (Public/Internal)

2. **ملء ملفات `domain-events.md`:**
   - توثيق جميع Events
   - تحديد Producers/Consumers

3. **مراجعة External Dependencies:**
   - التأكد من أنها `read-only`
   - توثيق Data Contracts

---

### المرحلة 2: التحسينات الطفيفة (الأولوية: متوسطة)

1. **مراجعة `location` service:**
   - تحديد: Reference Data أم قدرة مستقلة؟

2. **مراجعة `settings` service:**
   - توضيح: ما هي الإعدادات؟ Feature Flags؟ Config؟

3. **مراجعة `reports-analytics`:**
   - تحديد: Domain Service أم Infrastructure?

---

### المرحلة 3: إعادة الهيكلة (إذا لزم الأمر) (الأولوية: منخفضة)

1. **تقييم دمج Attendance Services:**
   - تحليل العلاقات بين `attendance-management`, `dismissal-management`, `excuse-management`
   - قرار: دمج أم إبقاء منفصلة؟

2. **تقييم `class-operations`:**
   - هل هي جزء من Attendance أم قدرة مستقلة؟

---

## 6. الخلاصة والتوصيات النهائية

### ✅ ما يعمل بشكل جيد:

1. **الفصل بين Kernel و Domain:** واضح ومنطقي ✅
2. **Database per Service:** تطبيق صحيح ✅
3. **External Data Dependencies:** موثقة كقراءة فقط ✅
4. **معظم الخدمات:** متماسكة وواضحة ✅

### ⚠️ مجالات التحسين:

1. **التوثيق:** ملء `boundaries.md` و `domain-events.md`
2. **بعض الخدمات:** تحتاج توضيح (location, settings, reports-analytics)
3. **Attendance Domain:** تقييم إمكانية الدمج

### 📋 الأولويات:

1. **عاجل:** توثيق Boundaries و Domain Events
2. **مهم:** توضيح location, settings, reports-analytics
3. **اختياري:** تقييم دمج Attendance Services

---

## 7. المراجع

- [Architecture Terminology](./Terminology.md)
- [Database per Service Architecture](../notes-proposal/tech-usage/db_per_service_architecture_laravel_okta.md)
- Service Extractability Principle (في Terminology.md)

---

**تاريخ الإنشاء:** 2025-01-26  
**آخر تحديث:** 2025-01-26