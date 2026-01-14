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
