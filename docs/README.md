# Okta Technical Documentation

## Overview

This directory contains the internal technical documentation for the Okta product. The documentation is organized into logical sections and follows a versioning scheme for tracking changes over time.

## Structure

The documentation is organized into the following sections:

- **00-base/** - Base documentation page and entry point
- **01-foundation/** - Foundational documentation (technical overview, engineering handbook, ADRs)
- **02-architecture/** - Architecture documentation (system architecture, domain models, data architecture, module communication)
- **03-development/** - Development documentation (local setup, GitHub workflow, CI/CD, testing)
- **04-integration/** - Integration documentation (API contracts, authentication/authorization)
- **05-operations/** - Operations documentation (observability, security)
- **06-releases/** - Release documentation (release notes, changelog)

## File Naming and Versioning

- Files use a version suffix in the format: `-v1`, `-v2`, `-v3`, etc.
- The first version of a document uses `-v1` suffix
- When creating a new version, increment the version number and create a new file
- Example: `technical-overview-v1.md`, `technical-overview-v2.md`

## Templates

Use the template file in `_templates/doc-page-template.md` when creating new documentation pages.

## Assets

- Images and other assets are stored in `assets/images/`
- Reference images using relative paths: `assets/images/filename.png`

## Export to PDF

See `export/README.md` for instructions on exporting documentation to PDF format.

## Getting Started

Start with the base page: [00-base/okta-docs-base-page-v1.md](00-base/okta-docs-base-page-v1.md)

