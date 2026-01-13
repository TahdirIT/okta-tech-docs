## Tech Transformation

### Old Project (Tahdir)
- Architecture: Monolith core-based architecture 
- Database: MySQL with Single-DB
- // Proposal: Cache :
- Framework: Laravel 11
- Frontend: Livewire 3 
- Messaging: Firebase Messaging
- Style: Traditional CSS
- Monitoring: Pulse 
### New Project (Okta v1 - In-scope decisions) 
- Architecture: Monolithic modular architecture (package: nwidart/laravel-modules)
- Database: PostgreSQL DB per Module
- // Proposal: Cache : Redis
- Framework: Laravel 12
- Frontend: Livewire 4 with Embedded React
- Messaging: Firebase Messaging
- Events: Pusher
- Style: SCSS
- Monitoring: Sentry.io + Nightwatch **(Proposal)**
* With applying possible standards help to transform to microservice architecture
### Feature Project (Okta - Out of Scope)
- Architecture: Microservices architecture
- Database: PostgreSQL DB per Microservice with DTOs / Contracts Layer
- External-apps integrations (From the partnerships)