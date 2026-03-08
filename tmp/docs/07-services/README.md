# Services Documentation

## Overview

This directory contains documentation for all services in the system, organized by service type (kernel and domain).

## Structure

Services are organized into two main categories:

- **kernel/** - Core services that provide foundational capabilities used across the system
- **domain/** - Domain-specific services that implement business capabilities

## Service Documentation Structure

Each service follows a standard documentation structure:

- **description.md** - Service overview and purpose
- **boundaries.md** - Service boundaries and responsibilities
- **business-rules.md** - Business rules and constraints
- **concepts.md** - Key concepts and terminology
- **domain-events.md** - Domain events published by the service
- **design-decisions.md** - Important design decisions (optional)
- **models/** - Data models documentation
  - **README.md** - Model overview and hierarchy
  - Individual model files

## Template

See `kernel/service-template/` for a complete template service directory structure that can be copied when creating documentation for a new service.

## Related Documentation

- Service definitions: `Preconception/services/`
- Architecture: `02-architecture/`
- API Contracts: `04-integration/api-contracts-v0.md`
