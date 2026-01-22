
<!-- ============================================ -->
<!-- File: print.md -->
<!-- ============================================ -->

# Technical Documentation

**Generated for PDF Export**

This document aggregates all technical documentation for the Okta platform.

---


<!-- Included from: business-features.md -->
## Business Feature

### 1. *With Clients:*
- Semester-based or term-based subscriptions → Annual or monthly subscriptions.
- The subscription included all features → Customized based on the services selected by the user.
- Conventional service subscriptions → App-store–like subscription experience.
- Subscription limited to a school or educational complex → Subscription available at teacher, school, or educational complex level.
- Integrating a third-party interactive community service (As an external-app) to offer each entity a dedicated private space, customized to its requirements.
- Each entity (school, educational complex) has its own dedicated landing page to provide a tailored experience and information relevant to that entity, with the ability to link with its own domain.

### 2. *With Partnerships:*
- Partnerships—under the traditional partnership agreement—require manual implementation within the platform and application. → Partnerships—after submitting a request and receiving team approval—are provided with an API that enables them to build their own integrations and exchange data through a flexible permission-based access system.

### 3. *With System:*
- The system is designed with a clear separation between a reusable platform Kernel Services and Domain-specific Services, allowing the kernel to function as a standalone SaaS foundation adaptable to various business domains.
- The visual style is developed with inspiration from the Digital Government Authority Platform Code standards, serving as a reference rather than a mandatory or full compliance framework. (كود المنصات ضمن هيئة الحكومة الرقمية). Visit: https://design.dga.gov.sa/.
<!-- End of: business-features.md -->


---


<!-- Included from: intent.md -->
## Intent
This document outlines the strategic and technical evolution from Tahdir to Okta, highlighting in-scope decisions for v1, future architectural directions, and key business transformation principles.
<!-- End of: intent.md -->


---


<!-- Included from: security.md -->
## Security

### Old Project (Tahdir)
- Authentication: Basic authentication mechanisms
- Authorization: Role-based access control (RBAC)
- Data Exposure: Sequential IDs exposed in URLs and APIs
- Encryption: Basic HTTPS/TLS
- Secrets Management: Environment variables managed via GitHub Actions secrets
- API Security: Basic API authentication
- Input Validation: Framework-level validation
- Security Headers: Basic security headers
- Vulnerability Scanning: Manual security reviews

### New Project (Okta v1 - In-scope decisions) 
- Authentication: Enhanced authentication with multi-factor authentication (MFA)
- Authorization: Role-based access control (RBAC) with fine-grained permissions
- Data Exposure: Using ULID as exposed ID in each model among services and publicity
- Encryption: End-to-end encryption for sensitive data, HTTPS/TLS
- Secrets Management: Secure secrets management with encrypted storage
- API Security: API authentication with JWT tokens, rate limiting
- Input Validation: Comprehensive input validation and sanitization
- Security Headers: Enhanced security headers (CSP, HSTS, X-Frame-Options)
- Vulnerability Scanning: Automated security scanning in CI/CD pipeline
- Security Monitoring: Security event logging and monitoring

### Feature Project (Okta - Out of Scope)
- Authentication: OAuth 2.0 / OpenID Connect (OIDC) with SSO
- Authorization: Attribute-based access control (ABAC) with policy engines
- Data Exposure: ULID with additional security layers for sensitive data
- Encryption: Field-level encryption, database encryption at rest
- Secrets Management: Secrets management with Vault / AWS Secrets Manager
- API Security: API Gateway with OAuth 2.0, API keys, mTLS
- Input Validation: Advanced validation with schema validation and WAF
- Security Headers: Comprehensive security headers with CSP policies
- Vulnerability Scanning: Continuous security scanning with SAST/DAST tools
- Security Monitoring: SIEM integration with real-time threat detection
- Zero-Trust Security: Zero-trust network architecture with service mesh
- Security Auditing: Comprehensive audit logging and compliance reporting
- Penetration Testing: Regular automated and manual penetration testing
- Security Compliance: SOC 2, ISO 27001 compliance frameworks

<!-- End of: security.md -->


---


<!-- Included from: technology-stack.md -->
## Technology Stack

### Old Project (Tahdir)
- Architecture: Monolith core-based architecture 
- Database: MySQL with Single-DB
- Cache: File Driver
- Framework: Laravel 11
- Frontend: Livewire 3 
- Messaging: Firebase Messaging
- Events: N/A
- Style: Traditional CSS
- Testing: PHPUnit for unit testing
- API Documentation: Basic API documentation
- Code Quality: Basic code standards
- Package Manager: Composer
- Build Tools: Laravel Mix
- Development Tools: Basic IDE support

### New Project (Okta v1 - In-scope decisions) 
- Architecture: Monolithic modular architecture (package: nwidart/laravel-modules - with applying possible standards help to transform to microservice architecture)
- Database: PostgreSQL DB per Module
- Cache: Redis
- Framework: Laravel 12
- Frontend: Livewire 4 with Embedded React
- Messaging: Firebase Messaging
- Events: Pusher
- Style: SCSS
- Testing: PHPUnit + Pest for unit and feature testing, React Testing Library for frontend
- API Documentation: OpenAPI/Swagger documentation
- Code Quality: PHPStan / Psalm for static analysis, ESLint for JavaScript
- Package Manager: Composer (PHP), npm/yarn (JavaScript)
- Build Tools: Vite for asset bundling
- Development Tools: Enhanced IDE support with type hints, debugging tools
- Queue System: Laravel Queue with Redis driver
- Task Scheduling: Laravel Scheduler
- File Storage: Local/S3-compatible storage
- Search: Basic database search
- Validation: Laravel Form Requests with custom rules

### Feature Project (Okta - Out of Scope)
- Architecture: Microservices architecture
- Database: PostgreSQL DB per Microservice with DTOs / Contracts Layer
- Cache: Distributed Redis cluster
- Framework: Laravel 12+ (per service), potential polyglot services
- Frontend: Livewire 4 with Embedded React, potential separate frontend services
- Messaging: Message queue (RabbitMQ / Apache Kafka) for inter-service communication
- Events: Event-driven architecture with event sourcing capabilities
- Style: SCSS with design system
- Testing: Comprehensive testing strategy (unit, integration, contract, E2E) with Pact for contract testing
- API Documentation: API Gateway with centralized documentation, GraphQL support
- Code Quality: Advanced static analysis, automated code review tools
- Package Manager: Service-specific package managers
- Build Tools: Multi-stage builds, optimized asset pipelines
- Development Tools: Service mesh tooling, distributed tracing tools
- Queue System: Distributed message queues per service
- Task Scheduling: Distributed task scheduling (Temporal / Temporal-like)
- File Storage: Object storage (S3) with CDN integration
- Search: Elasticsearch / OpenSearch for advanced search capabilities
- Validation: Schema validation with JSON Schema, API Gateway validation
- Service Communication: gRPC / REST APIs with service mesh
- API Gateway: Kong / AWS API Gateway / Envoy
- External-apps integrations: From the partnerships

<!-- End of: technology-stack.md -->


---


<!-- Included from: dev-ops.md -->
## Dev-Ops

### Old Project (Tahdir)
- CI/CD: Integrated with GitHub Actions
- Infrastructure: Traditional server management with 2 deployments (Test / Production) under one VM server
- Containerization: Not containerized
- Orchestration: N/A
- Environment Management: Manual environment setup
- Monitoring: Laravel Pulse
- Logging: File-based logging
- Backup: Manual database backups
- Version Control: Git with basic branching
- Security: Basic security practices

### New Project (Okta v1 - In-scope decisions) 
- CI/CD: GitHub Actions with automated testing and deployment
- Infrastructure: Infrastructure as Code (IaC) with Terraform / Ansible
- Containerization: Docker containers for applications
- Orchestration: Docker Compose for local development
- Environment Management: Environment variables with .env files
- Monitoring: Sentry.io + Nightwatch **(Proposal)**
- Logging: Centralized logging with structured logs (JSON format)
- Backup: Automated database backups with retention policies
- Version Control: Git Flow with feature branches and PR reviews
- Security: Automated security scanning in CI/CD pipeline
- Database Migrations: Automated migration runs in deployment pipeline
- Cache Management: Redis with automated cache warming strategies
* With applying possible standards help to transform to microservice architecture

### Feature Project (Okta - Out of Scope)
- CI/CD: Advanced CI/CD with GitOps (ArgoCD / Flux)
- Infrastructure: Cloud-native infrastructure (Kubernetes / ECS)
- Containerization: Multi-stage Docker builds with optimization
- Orchestration: Kubernetes for container orchestration
- Environment Management: ConfigMaps and Secrets management
- Monitoring: Distributed tracing (Jaeger / Zipkin) + APM (New Relic / Datadog)
- Logging: Centralized log aggregation (ELK Stack / Loki)
- Backup: Automated cross-region backups with disaster recovery
- Version Control: Trunk-based development with feature flags
- Security: Zero-trust security model with service mesh (Istio / Linkerd)
- Service Discovery: Service mesh with automatic service discovery
- Load Balancing: Advanced load balancing with health checks
- Auto-scaling: Horizontal Pod Autoscaling (HPA) based on metrics
- Blue-Green / Canary Deployments: Advanced deployment strategies
- Multi-region Deployment: Geographic distribution for high availability

<!-- End of: dev-ops.md -->


---

# Services


<!-- Included from: services\_index.md -->
# Services

## Contents


<!-- Included from: services\README.md -->
## Notes
External Data Dependencies describe data requirements,
not structural or database relationships.
<!-- End of: services\README.md -->



<!-- Included from: services\Terminology.md -->
# Architecture Terminology

This document defines the official terminology used across the system
architecture and documentation.

Its purpose is to establish a shared language and prevent ambiguity
during design, documentation, and future implementation phases.

---

## Service

A Service (or Module) represents a **business capability boundary**.
It encapsulates a coherent set of responsibilities, rules, and data
that serve a specific purpose within the system.

Services are the **only architectural units** that may evolve into
independently deployable microservices.

**Normative rule:**
> Services are extracted.  
> Models are never extracted.

---

## Module

A Module is a logical packaging unit used within a modular monolithic
architecture.

Modules:
- Represent service boundaries
- Are NOT deployment units
- Do NOT imply network isolation

A module may later be extracted into a microservice
when architectural and operational conditions allow.

---

## Model

A Model represents a **data concept owned by a single service**.
Models exist strictly within the boundary of their owning service
and must not be shared or reused directly by other services.

Models are used to express:
- Data structure
- Domain behavior
- State transitions

Models are **not** architectural or deployment boundaries.

---

## Reference Model

A Reference Model represents **shared, relatively stable data**
used primarily for classification, configuration, or lookup.

### Characteristics
- Read-heavy
- Low behavioral complexity
- Infrequent changes
- Widely consumed across services

### Examples
- Country
- Region
- City
- Education Level

**Important:**
> Reference Models do not define microservice boundaries.

---

## Operational Model

An Operational Model represents **business operations, workflows,
or stateful processes** with a clear lifecycle and business rules.

### Characteristics
- High behavioral complexity
- Frequent state changes
- Central to business workflows
- Often emits domain events

### Examples
- Attendance
- Call
- Dismissal
- Conduct Case

Operational Models indicate **business behavior**,
not deployment units.

---

## Internal Association

An Internal Association describes a logical relationship between
models **within the same service boundary**.

Internal associations:
- Are allowed
- May be documented explicitly
- Must not reference external services or modules

---

## External Data Dependency

An External Data Dependency represents a **read-only dependency**
on data owned by another service.

External data dependencies:
- Do NOT imply database relationships
- Do NOT imply ORM associations
- Do NOT allow cross-service joins
- Represent required data context only

**Key principle:**
> Services depend on data, not on databases.

---

## Domain

The Domain represents the **core business logic** of a service.
It defines business rules, policies, invariants, and domain events,
independent of technical implementation details.

The Domain must not depend on:
- Frameworks
- Databases
- APIs
- Infrastructure concerns

---

## Domain Event

A Domain Event represents a **significant business fact**
that occurred within a domain.

Domain events:
- Describe what happened
- Are immutable
- Carry no assumptions about consumers
- Do not trigger actions directly

Examples:
- AttendanceMarked
- StudentSuspended
- GradeFinalized

---

## Architectural Signal

An Architectural Signal is a **non-decisive indicator**
used to reason about system structure and future evolution.

Examples of architectural signals:
- Model classification (Reference vs Operational)
- Event frequency
- Data volatility

Architectural signals:
- Do NOT mandate architectural decisions
- Are used for evaluation, not enforcement

---

## Service Extractability Principle

A service’s suitability for extraction into a microservice
is determined by the **behavior it encapsulates**, not by
individual models.

However, the dominant model types within a service
provide strong architectural signals:

- Services dominated by Reference Models  
  → Typically remain shared modules

- Services containing Operational Models with rich behavior  
  → Potential microservice candidates (in later stages)

---

## Normative Summary

```text
Models are never extracted.
Services are extracted.
Model types are signals, not decisions.
External dependencies are data-based, not relational.

<!-- End of: services\Terminology.md -->



<!-- End of: services\_index.md -->


---

# Notes & Proposals


<!-- Included from: notes-proposal\_index.md -->
# Notes Proposal

## Contents


<!-- Included from: notes-proposal\Domain Events Naming.md -->

<!-- End of: notes-proposal\Domain Events Naming.md -->



<!-- Included from: notes-proposal\DTO.md -->
الحل الصحيح (ليس الآن)

في مرحلة Microservices لاحقًا:

لديك 3 أدوات:

DTOs / Contracts

Read Models

Anti-Corruption Layer (ACL)

لكن الآن:
✔️ الاكتفاء بـ Reference IDs
✔️ لا مشاركة Models
✔️ لا علاقات Cross-Service ORM
<!-- End of: notes-proposal\DTO.md -->



<!-- Included from: notes-proposal\service-governance.md -->
## Service Ownership Model

## RACI Templates

## Change Management Framework

## SLA & SLO Definitions

## Escalation Paths

## Incident & Problem Management

## Governance Committees

## Product Governance

//Proposal

Product governance is addressed through a **Minimum Viable Governance (MVG)** model, deliberately 
aligned with the current stage of the platform and the size of the core team.

This model ensures clear ownership, accountability, and decision-making authority, while remaining 
lightweight, pragmatic, and adaptable. It is intentionally designed to evolve into a more formal 
and comprehensive governance framework as the platform scales, operational complexity increases, 
and additional stakeholders are introduced.

The product itself is **functionally mature**, building on capabilities and workflows proven in a 
previous production system. Accordingly, the current phase places stronger emphasis on **technical 
transformation, modularization, and architectural modernization**, while core business features, 
rules, and workflows are documented and maintained separately in `business-features.md`.
<!-- End of: notes-proposal\service-governance.md -->



<!-- Included from: notes-proposal\service-separation-recommendations.md -->
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
| `access-control` | ✅ جيد | نظام الصلاحيات المركزي |
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
| `tenant-management` | ✅ جيد | إدارة المدارس والمجمعات |
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
- Role definitions (from access-control) - read-only
- School data (from tenant-management) - read-only

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
      - access-control
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
      - tenant-management
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
   - مثال: `employee-management` يعتمد على `tenant-management` والعكس
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
<!-- End of: notes-proposal\service-separation-recommendations.md -->



<!-- Included from: notes-proposal\techs.md -->
- Laravel Events
- Redis Streams
- Database Outbox Pattern
<!-- End of: notes-proposal\techs.md -->



<!-- End of: notes-proposal\_index.md -->


---

*End of Document*
