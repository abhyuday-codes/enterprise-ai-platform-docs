---
title: Repository Structure
document_id: ENG-002
version: 1.0.0
status: Approved
owner: Engineering
classification: Internal
phase: Engineering
last_updated: YYYY-MM-DD
---

# Repository Structure

## Executive Summary

The Enterprise AI Platform follows a **modular monorepo architecture** that enables independent service development while maintaining shared engineering standards, tooling, governance, and release management.

The repository is organized around business domains rather than technologies. Every deployable service, shared package, SDK, infrastructure component, and operational asset has a clearly defined location and ownership.

The repository structure is designed for long-term maintainability, enterprise scalability, and developer productivity.

---

# Purpose

This document defines:

- Repository organization
- Directory standards
- Service structure
- Package structure
- Naming conventions
- Dependency rules
- Ownership model
- Documentation organization
- Repository governance

---

# Design Principles

The repository shall be:

- Modular
- Discoverable
- Consistent
- Scalable
- Domain Driven
- Automation Friendly
- Documentation First
- Testable
- Governed

---

# Repository Overview

```text
enterprise-ai-platform/

├── apps/
├── services/
├── packages/
├── sdk/
├── agents/
├── prompts/
├── workflows/
├── mcp/
├── infrastructure/
├── deployments/
├── configs/
├── scripts/
├── tools/
├── tests/
├── docs/
├── examples/
├── assets/
├── .github/
├── .devcontainer/
├── .vscode/
├── pyproject.toml
├── uv.lock
├── Makefile
├── README.md
├── CONTRIBUTING.md
├── CHANGELOG.md
└── LICENSE
```

---

# Repository Layers

```text
Applications
        │
        ▼
Microservices
        │
        ▼
Shared Packages
        │
        ▼
Infrastructure Libraries
        │
        ▼
Infrastructure
```

Dependencies flow downward only.

---

# apps/

Contains user-facing applications.

```text
apps/

portal/
admin/
playground/
desktop/
cli/
```

Applications orchestrate services and SDKs but do not contain business logic owned by backend services.

---

# services/

Contains independently deployable backend services.

```text
services/

api-gateway/
ai-gateway/
identity-service/
authorization-service/
context-service/
knowledge-service/
memory-service/
prompt-service/
workflow-service/
agent-service/
mcp-gateway/
governance-service/
evaluation-service/
audit-service/
notification-service/
configuration-service/
search-service/
administration-service/
```

Each service owns:

- APIs
- Domain logic
- Persistence
- Events
- Configuration
- Tests
- Documentation

---

# Standard Service Structure

Every service follows the same internal layout.

```text
service-name/

src/

    api/
    application/
    domain/
    infrastructure/
    integrations/
    repositories/
    events/
    models/
    middleware/
    security/
    telemetry/
    workers/

tests/

migrations/

configs/

docs/

Dockerfile

pyproject.toml

README.md
```

No service may deviate without an approved ADR.

---

# packages/

Reusable platform libraries.

```text
packages/

core/
common/
configuration/
database/
events/
security/
telemetry/
logging/
exceptions/
ai/
mcp/
workflow/
search/
vector/
cache/
testing/
utils/
```

Packages shall remain framework-agnostic whenever practical.

---

# sdk/

Official SDKs.

```text
sdk/

python/
typescript/
java/
dotnet/
go/
```

SDKs expose public APIs for external developers.

---

# agents/

Built-in enterprise AI agents.

```text
agents/

developer/
documentation/
architecture/
security/
operations/
reviewer/
knowledge/
```

Each agent maintains:

- Configuration
- Prompt templates
- Skills
- Policies
- Tests

---

# prompts/

Governed prompt assets.

```text
prompts/

system/
templates/
evaluation/
classification/
summarization/
reasoning/
enterprise/
```

Prompts are version-controlled and require approval before publication.

---

# workflows/

Workflow definitions.

```text
workflows/

approval/
documentation/
deployment/
review/
evaluation/
automation/
```

Workflows are treated as platform assets and support versioning.

---

# mcp/

Model Context Protocol resources.

```text
mcp/

servers/
clients/
registry/
schemas/
adapters/
tools/
```

Supports both internal and customer-provided MCP implementations.

---

# infrastructure/

Infrastructure as Code.

```text
infrastructure/

terraform/
helm/
kubernetes/
networking/
security/
monitoring/
storage/
```

No manual infrastructure configuration shall be required in production.

---

# deployments/

Environment-specific deployment configurations.

```text
deployments/

local/
development/
testing/
staging/
production/
on-prem/
air-gapped/
```

Deployment profiles inherit common defaults and override environment-specific settings.

---

# configs/

Shared configuration.

```text
configs/

logging/
telemetry/
grafana/
prometheus/
linting/
formatting/
security/
```

---

# scripts/

Engineering automation.

```text
scripts/

bootstrap.py
build.py
release.py
generate-sdk.py
validate-docs.py
```

Scripts shall be idempotent where practical.

---

# tools/

Internal engineering utilities.

```text
tools/

migration/
benchmark/
profiling/
diagnostics/
generators/
```

Tools are not deployed to production.

---

# tests/

Platform-level testing.

```text
tests/

unit/
integration/
contract/
performance/
load/
security/
e2e/
chaos/
fixtures/
```

Shared test utilities belong under `packages/testing`.

---

# docs/

Project documentation.

```text
docs/

01-product/
02-functional-specification/
03-architecture/
04-engineering/
05-implementation/
06-operations/
07-adr/
templates/
assets/
```

Documentation is version-controlled and reviewed alongside code.

---

# examples/

Reference implementations.

```text
examples/

api/
rag/
agent/
workflow/
mcp/
sdk/
```

Examples are executable and continuously validated.

---

# assets/

Shared non-code resources.

```text
assets/

images/
diagrams/
icons/
branding/
templates/
```

---

# Naming Conventions

## Directories

Use kebab-case.

Examples:

```text
knowledge-service
workflow-service
ai-gateway
```

---

## Python Packages

Use snake_case.

Examples:

```python
enterprise_ai
knowledge_service
workflow_engine
```

---

## Classes

Use PascalCase.

```python
KnowledgeRepository
WorkflowEngine
PromptResolver
```

---

## Functions

Use snake_case.

```python
create_workflow()
resolve_prompt()
store_memory()
```

---

## Constants

Use UPPER_SNAKE_CASE.

```python
DEFAULT_TIMEOUT

MAX_TOKEN_LIMIT
```

---

# Dependency Rules

Allowed:

```text
Application
      ↓
Service
      ↓
Shared Package
      ↓
Infrastructure Library
```

Not Allowed:

```text
Service A
      ↓
Service B Source Code
```

Services communicate only through:

- REST APIs
- gRPC
- Event Bus
- Official SDKs

---

# Ownership

Every service shall define:

- Technical Owner
- Product Owner
- Architecture Reviewer
- Security Reviewer

Ownership is managed using:

```text
CODEOWNERS
```

---

# Documentation Requirements

Every service shall include:

- README
- Architecture Overview
- API Documentation
- Configuration Guide
- Deployment Guide
- Runbook
- Changelog

---

# Generated Code

Generated artifacts belong under:

```text
generated/

openapi/
grpc/
clients/
```

Generated files shall never be manually modified.

---

# Repository Governance

Repository-wide changes require:

- Architecture approval
- Engineering approval
- Documentation updates
- Migration strategy
- Backward compatibility assessment

---

# Design Constraints

The repository shall never:

- Share databases between services
- Duplicate shared libraries
- Introduce circular dependencies
- Store secrets
- Mix generated and handwritten code
- Couple services through source-code references

---

# Success Criteria

The repository is considered well-structured when:

- New services can be scaffolded consistently.
- Shared functionality is reusable.
- Developers can quickly locate code.
- CI/CD can operate uniformly across services.
- Repository growth does not reduce maintainability.
- Documentation and implementation remain synchronized.

---

# Dependencies

- ENG-001 Engineering Foundation
- Technology Stack
- Microservice Architecture

---

# Related Documents

- ENG-003 Coding Standards
- ENG-004 API Standards
- ENG-005 Database Standards
- ENG-006 Event Standards
- ENG-007 Testing Strategy
- ENG-008 Configuration Management

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
| DevOps Lead | Pending |