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
- [Style Guide](#style-guide)
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

## Style Guide

The documentation follows consistent style standards for colors, icons, typography, and formatting to ensure a professional and cohesive appearance across all documents.

| Document | Description | Link |
|----------|-------------|------|
| Style Guide | Documentation style standards including colors, icons, typography, and formatting guidelines | [style-guide-v0.md](style-guide-v0.md) |

---

## Foundation Documentation

| Document | Description | Link |
|----------|-------------|------|
| Technical Overview | High-level technical overview of the Okta product | [technical-overview-v0.md](../01-foundation/technical-overview-v0.md) |
| Engineering Handbook | Engineering practices and guidelines | [engineering-handbook-v0.md](../01-foundation/engineering-handbook-v0.md) |
| ADR Index | Architecture Decision Records index | [adr-index-v0.md](../01-foundation/adr-index-v0.md) |

---

## Architecture Documentation

| Document | Description | Link |
|----------|-------------|------|
| System Architecture (Modular) | Modular architecture overview and design | [system-architecture-modular-v0.md](../02-architecture/system-architecture-modular-v0.md) |
| Domain Model & Bounded Contexts | Domain-driven design models and bounded contexts | [domain-model-bounded-contexts-v0.md](../02-architecture/domain-model-bounded-contexts-v0.md) |
| Data Architecture & ERD | Data architecture and entity relationship diagrams | [data-architecture-erd-v0.md](../02-architecture/data-architecture-erd-v0.md) |
| Module Communication | Inter-module communication patterns and protocols | [module-communication-v0.md](../02-architecture/module-communication-v0.md) |

---

## Development Documentation

| Document | Description | Link |
|----------|-------------|------|
| Local Development Setup | Instructions for setting up local development environment | [local-development-setup-v0.md](../03-development/local-development-setup-v0.md) |
| GitHub Workflow | GitHub workflow and branching strategy | [github-workflow-v0.md](../03-development/github-workflow-v0.md) |
| CI/CD Pipeline | Continuous Integration and Continuous Deployment pipeline | [ci-cd-pipeline-v0.md](../03-development/ci-cd-pipeline-v0.md) |
| Testing Strategy | Testing approach, strategies, and best practices | [testing-strategy-v0.md](../03-development/testing-strategy-v0.md) |

---

## Integration Documentation

| Document | Description | Link |
|----------|-------------|------|
| API Contracts | API contracts and specifications | [api-contracts-v0.md](../04-integration/api-contracts-v0.md) |
| Authentication & Authorization | Authentication, authorization, and permissions | [authn-authz-permissions-v0.md](../04-integration/authn-authz-permissions-v0.md) |

---

## Operations Documentation

| Document | Description | Link |
|----------|-------------|------|
| Observability | Logging, metrics, and tracing | [observability-logs-metrics-tracing-v0.md](../05-operations/observability-logs-metrics-tracing-v0.md) |
| Security Guidelines | Security guidelines and threat model | [security-guidelines-threat-model-v0.md](../05-operations/security-guidelines-threat-model-v0.md) |

---

## Releases Documentation

| Document | Description | Link |
|----------|-------------|------|
| Release Notes & Changelog | Release notes and changelog | [release-notes-changelog-v0.md](../06-releases/release-notes-changelog-v0.md) |

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

### Style Guide
- [Style Guide](style-guide-v0.md)

### Foundation
- [Technical Overview](../01-foundation/technical-overview-v0.md)
- [Engineering Handbook](../01-foundation/engineering-handbook-v0.md)
- [ADR Index](../01-foundation/adr-index-v0.md)

### Architecture
- [System Architecture (Modular)](../02-architecture/system-architecture-modular-v0.md)
- [Domain Model & Bounded Contexts](../02-architecture/domain-model-bounded-contexts-v0.md)
- [Data Architecture & ERD](../02-architecture/data-architecture-erd-v0.md)
- [Module Communication](../02-architecture/module-communication-v0.md)

### Development
- [Local Development Setup](../03-development/local-development-setup-v0.md)
- [GitHub Workflow](../03-development/github-workflow-v0.md)
- [CI/CD Pipeline](../03-development/ci-cd-pipeline-v0.md)
- [Testing Strategy](../03-development/testing-strategy-v0.md)

### Integration
- [API Contracts](../04-integration/api-contracts-v0.md)
- [Authentication & Authorization](../04-integration/authn-authz-permissions-v0.md)

### Operations
- [Observability](../05-operations/observability-logs-metrics-tracing-v0.md)
- [Security Guidelines](../05-operations/security-guidelines-threat-model-v0.md)

### Releases
- [Release Notes & Changelog](../06-releases/release-notes-changelog-v0.md)

