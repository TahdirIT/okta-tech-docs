# Okta Technical Documentation - Base Page

## Document Metadata

- **Version:** 1.0
- **Status:** Draft
- **Owner:** Technical Documentation Team
- **Last Updated:** 2026-01-08
- **Related ADRs:** N/A

---

## Table of Contents

- [Overview](#overview)
- [Documentation Structure](#documentation-structure)
- [Foundation Documentation](#foundation-documentation)
- [Architecture Documentation](#architecture-documentation)
- [Development Documentation](#development-documentation)
- [Integration Documentation](#integration-documentation)
- [Operations Documentation](#operations-documentation)
- [Releases Documentation](#releases-documentation)
- [PDF Export](#pdf-export)
- [Sub-pages](#sub-pages)

---

## Overview

This is the main entry point for the Okta technical documentation. The documentation covers all aspects of the Okta product, including architecture, development, integration, operations, and releases.

**Technology Stack:**
- Laravel 12
- Livewire 4-beta
- GitHub for version control

**Architecture:**
- Current: Laravel Modular Architecture
- Future: Microservices (each module/microservice as a separate project)

---

## Documentation Structure

The documentation is organized into the following sections:

1. **Foundation** - Core technical overview, engineering handbook, and ADRs
2. **Architecture** - System architecture, domain models, data architecture, and module communication
3. **Development** - Local development setup, GitHub workflow, CI/CD, and testing
4. **Integration** - API contracts and authentication/authorization
5. **Operations** - Observability, logging, metrics, tracing, and security
6. **Releases** - Release notes and changelog

---

## Foundation Documentation

| Document | Description | Link |
|----------|-------------|------|
| Technical Overview | High-level technical overview of the Okta product | [technical-overview-v1.md](../01-foundation/technical-overview-v1.md) |
| Engineering Handbook | Engineering practices and guidelines | [engineering-handbook-v1.md](../01-foundation/engineering-handbook-v1.md) |
| ADR Index | Architecture Decision Records index | [adr-index-v1.md](../01-foundation/adr-index-v1.md) |

---

## Architecture Documentation

| Document | Description | Link |
|----------|-------------|------|
| System Architecture (Modular) | Modular architecture overview and design | [system-architecture-modular-v1.md](../02-architecture/system-architecture-modular-v1.md) |
| Domain Model & Bounded Contexts | Domain-driven design models and bounded contexts | [domain-model-bounded-contexts-v1.md](../02-architecture/domain-model-bounded-contexts-v1.md) |
| Data Architecture & ERD | Data architecture and entity relationship diagrams | [data-architecture-erd-v1.md](../02-architecture/data-architecture-erd-v1.md) |
| Module Communication | Inter-module communication patterns and protocols | [module-communication-v1.md](../02-architecture/module-communication-v1.md) |

---

## Development Documentation

| Document | Description | Link |
|----------|-------------|------|
| Local Development Setup | Instructions for setting up local development environment | [local-development-setup-v1.md](../03-development/local-development-setup-v1.md) |
| GitHub Workflow | GitHub workflow and branching strategy | [github-workflow-v1.md](../03-development/github-workflow-v1.md) |
| CI/CD Pipeline | Continuous Integration and Continuous Deployment pipeline | [ci-cd-pipeline-v1.md](../03-development/ci-cd-pipeline-v1.md) |
| Testing Strategy | Testing approach, strategies, and best practices | [testing-strategy-v1.md](../03-development/testing-strategy-v1.md) |

---

## Integration Documentation

| Document | Description | Link |
|----------|-------------|------|
| API Contracts | API contracts and specifications | [api-contracts-v1.md](../04-integration/api-contracts-v1.md) |
| Authentication & Authorization | Authentication, authorization, and permissions | [authn-authz-permissions-v1.md](../04-integration/authn-authz-permissions-v1.md) |

---

## Operations Documentation

| Document | Description | Link |
|----------|-------------|------|
| Observability | Logging, metrics, and tracing | [observability-logs-metrics-tracing-v1.md](../05-operations/observability-logs-metrics-tracing-v1.md) |
| Security Guidelines | Security guidelines and threat model | [security-guidelines-threat-model-v1.md](../05-operations/security-guidelines-threat-model-v1.md) |

---

## Releases Documentation

| Document | Description | Link |
|----------|-------------|------|
| Release Notes & Changelog | Release notes and changelog | [release-notes-changelog-v1.md](../06-releases/release-notes-changelog-v1.md) |

---

## PDF Export

This documentation can be exported to PDF format for offline viewing and distribution.

### Export Instructions

For detailed instructions on exporting this documentation to PDF, please refer to:
- [PDF Export Instructions](../export/README.md)

### Export Options

1. **Option A: VS Code / Markdown PDF Extension**
   - Install the Markdown PDF extension in VS Code
   - Right-click on this file and select "Markdown PDF: Export (pdf)"
   - The extension will generate a PDF with all linked sub-pages and images

2. **Option B: Pandoc**
   - Install Pandoc on your system
   - Use Pandoc command-line tool to convert markdown to PDF
   - See export/README.md for detailed commands

### Export Considerations

- Ensure all sub-pages are accessible before exporting
- Verify all image paths are correct
- Review the generated PDF for formatting issues
- The export should include all linked sub-pages and referenced images

---

## Images

- ![Okta Architecture Overview](assets/images/okta-architecture-overview.png)
- ![Documentation Structure](assets/images/documentation-structure.png)

---

## Sub-pages

### Foundation
- [Technical Overview](../01-foundation/technical-overview-v1.md)
- [Engineering Handbook](../01-foundation/engineering-handbook-v1.md)
- [ADR Index](../01-foundation/adr-index-v1.md)

### Architecture
- [System Architecture (Modular)](../02-architecture/system-architecture-modular-v1.md)
- [Domain Model & Bounded Contexts](../02-architecture/domain-model-bounded-contexts-v1.md)
- [Data Architecture & ERD](../02-architecture/data-architecture-erd-v1.md)
- [Module Communication](../02-architecture/module-communication-v1.md)

### Development
- [Local Development Setup](../03-development/local-development-setup-v1.md)
- [GitHub Workflow](../03-development/github-workflow-v1.md)
- [CI/CD Pipeline](../03-development/ci-cd-pipeline-v1.md)
- [Testing Strategy](../03-development/testing-strategy-v1.md)

### Integration
- [API Contracts](../04-integration/api-contracts-v1.md)
- [Authentication & Authorization](../04-integration/authn-authz-permissions-v1.md)

### Operations
- [Observability](../05-operations/observability-logs-metrics-tracing-v1.md)
- [Security Guidelines](../05-operations/security-guidelines-threat-model-v1.md)

### Releases
- [Release Notes & Changelog](../06-releases/release-notes-changelog-v1.md)

