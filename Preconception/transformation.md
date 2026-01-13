# Transformation



## Intent
This document outlines the strategic and technical evolution from Tahdir to Okta, highlighting in-scope decisions for v1, future architectural directions, and key business transformation principles.



## Tech
### Old Project (Tahdir)
    - Architecture: Monolith core-based architecture 
    - Database: MySQL with Single-DB
    - // Proposal: Cache :
    - Framework: Laravel 11
    - Frontend: Livewire 3 
    - Messaging: Firebase Messaging
    - // Proposal: Style: Traditional CSS
    - Monitoring: Pulse 
### New Project (Okta v1 - In-scope decisions) 
    - Architecture: Monolithic modular architecture (package: nwidart/laravel-modules)
    - Database: PostgreSQL DB per Module
    - // Proposal: Cache : Redis
    - Framework: Laravel 12
    - Frontend: Livewire 4 with Embedded React
    - Messaging: Firebase Messaging + Pusher
    - Style: SCSS
    - // Proposal: Monitoring: Sentry.io
    - // Proposal: Monitoring: Nightwatch
    * With applying possible standards help to transform to microservice architecture
### Feature Project (Okta - Out of Scope)
    - Architecture: Microservices architecture
    - Database: PostgreSQL DB per Microservice with DTOs / Contracts Layer
    - External-apps integrations (From the partnerships)



## Business Feature
### 1. *With Clients:*
    - Semester-based or term-based subscriptions → Annual or monthly subscriptions.
    - The subscription included all features → Customized based on the services selected by the user.
    - Conventional service subscriptions → App-store–like subscription experience.
    - Subscription limited to a school or educational complex → Subscription available at teacher, school, or educational complex level.
    - Integrating a third-party interactive community service (As an external-app) to offer each entity a dedicated private space, customized to its requirements.
### 2. *With Partnerships:*
    - Partnerships—under the traditional partnership agreement—require manual implementation within the platform and application. → Partnerships—after submitting a request and receiving team approval—are provided with an API that enables them to build their own integrations and exchange data through a flexible permission-based access system.
### 3. *With System:*
    - The system is designed with a clear separation between a reusable platform Kernel Services and Domain-specific Services, allowing the kernel to function as a standalone SaaS foundation adaptable to various business domains.
    - The visual style is developed with inspiration from the Digital Government Authority Platform Code standards, serving as a reference rather than a mandatory or full compliance framework. (كود المنصات ضمن هيئة الحكومة الرقمية). Visit: https://design.dga.gov.sa/.



## Security
- Using ulid as exposed id in each model among services and publicity.