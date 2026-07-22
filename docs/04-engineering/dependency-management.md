---
title: Dependency Management
document_id: ENG-008
version: 1.0.0
status: Approved
owner: Engineering
classification: Internal
phase: Engineering
last_updated: YYYY-MM-DD
---

# Dependency Management

## Executive Summary

This document establishes the standards for managing software dependencies across the Enterprise AI Platform.

Dependencies introduce functionality, security risks, operational risks, licensing obligations, and maintenance costs. Every dependency shall be evaluated, approved, monitored, updated, and governed throughout its lifecycle.

The platform adopts a **minimal dependency philosophy** to maximize security, maintainability, and long-term stability.

---

# Purpose

This document defines:

- Dependency philosophy
- Dependency classification
- Package management
- Versioning policy
- Approval workflow
- Security scanning
- License compliance
- Dependency lifecycle
- Software Bill of Materials (SBOM)
- Governance

---

# Dependency Philosophy

Every dependency shall provide measurable value.

Before introducing a dependency, engineers shall evaluate:

- Business value
- Engineering value
- Maintenance cost
- Security impact
- Licensing
- Community health
- Long-term viability

The best dependency is the one that is not required.

---

# Dependency Principles

Dependencies shall be:

- Justified
- Maintained
- Secure
- Versioned
- Observable
- Replaceable
- Well documented

Unused dependencies shall be removed promptly.

---

# Dependency Categories

## Runtime Dependencies

Required by production services.

Examples:

- FastAPI
- SQLAlchemy
- OpenTelemetry
- Redis Client

---

## Development Dependencies

Used only during development.

Examples:

- Ruff
- pytest
- mypy
- pre-commit

Development dependencies shall never be included in production container images.

---

## Build Dependencies

Required during build.

Examples:

- uv
- Alembic
- Protobuf Compiler

---

## Infrastructure Dependencies

Infrastructure tooling.

Examples:

- Terraform
- Helm
- Docker

---

## AI Dependencies

Libraries used for AI capabilities.

Examples:

- OpenAI SDK
- Anthropic SDK
- Azure OpenAI SDK
- Transformers

AI dependencies shall remain isolated behind provider abstraction layers.

---

# Package Manager

Python dependency management shall use:

```text
uv
```

Repository requirements:

- Locked dependencies
- Deterministic builds
- Reproducible environments

Direct dependency installation using:

```text
pip install
```

is prohibited outside isolated development scenarios.

---

# Dependency Declaration

Dependencies shall be declared only in:

```text
pyproject.toml
```

Lock files shall be committed:

```text
uv.lock
```

Lock files are mandatory.

---

# Versioning Policy

The platform follows Semantic Versioning.

Allowed version strategy:

```text
MAJOR.MINOR.PATCH
```

Example:

```
2.5.1
```

Avoid floating dependency versions.

Bad:

```text
*
latest
>=1
```

Preferred:

```text
~=2.5

==2.5.3

^2.5
```

Version ranges shall balance stability with security updates.

---

# Approved Dependency Sources

Dependencies shall originate only from approved sources.

Examples:

- PyPI
- Official vendor repositories
- Internal package registry

Unverified package sources are prohibited.

---

# Dependency Evaluation

Before approval, evaluate:

- Project maturity
- Community adoption
- Release cadence
- Documentation quality
- Issue responsiveness
- Security history
- Maintenance activity

Archived or abandoned projects shall not be adopted.

---

# Security Requirements

Every dependency shall undergo:

- Vulnerability scanning
- License scanning
- Supply chain verification
- Integrity validation

Critical vulnerabilities block production releases.

---

# Vulnerability Management

Scanning tools include:

- Trivy
- OSV Scanner
- Dependabot
- GitHub Advisory Database

Critical findings shall be remediated immediately.

---

# License Compliance

Approved license examples:

- MIT
- Apache-2.0
- BSD

Restricted licenses require Legal approval.

Examples:

- GPL
- AGPL
- SSPL

Every dependency shall have an identified license.

---

# Software Bill of Materials (SBOM)

Every release shall generate an SBOM.

Recommended formats:

- SPDX
- CycloneDX

SBOMs shall include:

- Package
- Version
- License
- Source
- Hash

SBOMs become release artifacts.

---

# Internal Packages

Shared platform libraries belong under:

```text
packages/
```

Examples:

```
packages/core
packages/database
packages/events
packages/security
packages/telemetry
packages/ai
```

Applications shall reuse internal packages before introducing external alternatives.

---

# Dependency Scope

Dependencies shall have the narrowest possible scope.

Example:

Good

```
service-a

↓

SQLAlchemy
```

Avoid installing unrelated packages globally across services.

---

# Dependency Updates

Dependency updates shall be:

- Planned
- Tested
- Documented
- Reviewed

Production upgrades require automated validation.

---

# Breaking Updates

Major version upgrades require:

- Compatibility assessment
- Migration plan
- Regression testing
- Architecture review

Breaking upgrades require an ADR where platform-wide impact exists.

---

# Deprecated Dependencies

Deprecated dependencies shall:

- Be documented
- Include migration guidance
- Have a removal timeline

Unsupported software shall not remain in production.

---

# AI Provider SDKs

AI provider SDKs shall remain isolated.

Example:

```
AI Gateway

↓

Provider Adapter

↓

OpenAI SDK

Anthropic SDK

Gemini SDK

Azure OpenAI SDK
```

Business logic shall never directly depend on vendor SDKs.

---

# Dependency Isolation

Service-specific dependencies shall remain within that service.

Shared dependencies belong only in reusable packages.

Avoid unnecessary coupling.

---

# Container Images

Production container images shall:

- Minimize installed packages
- Remove build tooling
- Exclude test dependencies
- Use non-root users
- Scan for vulnerabilities

Slim base images are preferred.

---

# Dependency Monitoring

Continuously monitor:

- Vulnerabilities
- New releases
- End-of-life announcements
- License changes
- Security advisories

Monitoring shall be automated.

---

# Automated Updates

Automation may create dependency update pull requests.

Updates shall still require:

- Testing
- Review
- Approval

Automatic production deployment of dependency updates is prohibited.

---

# Documentation

Every external dependency shall document:

- Purpose
- Owner
- Version
- Upgrade process
- Alternatives
- Security considerations

Platform-critical dependencies require architecture documentation.

---

# Governance

Introducing a new dependency requires:

- Engineering review
- Security review
- License validation
- Architecture approval (for platform-wide dependencies)

Platform-wide dependency changes require communication across engineering teams.

---

# Prohibited Practices

The following are prohibited:

- Floating versions
- Unmaintained libraries
- Direct vendor SDK usage in business logic
- Duplicate libraries providing identical functionality
- Production dependencies without lock files
- Dependencies from untrusted repositories
- Ignoring critical vulnerabilities
- Manual modification of lock files

---

# Success Criteria

Dependency management is successful when:

- Builds are deterministic.
- Dependency trees remain minimal.
- Security vulnerabilities are detected early.
- Licensing obligations are met.
- Platform upgrades are predictable.
- External dependencies remain replaceable.

---

# Dependencies

- ENG-001 Engineering Foundation
- ENG-002 Repository Structure
- ENG-003 Coding Standards
- ENG-007 Configuration Management

---

# Related Documents

- ENG-009 Testing Strategy
- ENG-010 Git Workflow
- ENG-012 CI/CD Standards
- ENG-013 Secure SDLC
- Technology Stack
- Security Architecture

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0.0 | YYYY-MM-DD | Engineering | Initial version |

---

# Approval

| Role | Status |
|------|--------|
| Chief Architect | Approved |
| Engineering Director | Approved |
| Platform Lead | Approved |
| Security Lead | Approved |
| Legal & Compliance | Pending |