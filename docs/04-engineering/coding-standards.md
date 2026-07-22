---
title: Coding Standards
document_id: ENG-003
version: 1.0.0
status: Approved
owner: Engineering
classification: Internal
phase: Engineering
last_updated: YYYY-MM-DD
---

# Coding Standards

## Executive Summary

This document defines the mandatory coding standards for all software developed within the Enterprise AI Platform. These standards ensure consistency, maintainability, security, readability, and long-term scalability across every repository, service, package, and SDK.

Coding standards are **mandatory** and apply to all contributors, regardless of programming language or team.

---

# Purpose

This document defines:

- General coding principles
- Python development standards
- Project organization
- Naming conventions
- Type safety
- Dependency injection
- Error handling
- Logging
- Configuration usage
- Documentation
- Code quality expectations
- Review requirements

---

# Engineering Philosophy

Code should be:

- Simple
- Readable
- Predictable
- Maintainable
- Testable
- Secure
- Observable
- Extensible

Readable code is preferred over clever code.

---

# General Principles

## SOLID

Every implementation should follow SOLID principles.

- Single Responsibility
- Open/Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

---

## DRY

Avoid unnecessary duplication.

Common functionality belongs in shared packages.

---

## KISS

Prefer the simplest implementation that satisfies the requirements.

---

## YAGNI

Do not implement speculative features.

Build only what is required by the approved specification.

---

## Composition Over Inheritance

Prefer composition unless inheritance provides a clear architectural benefit.

---

# Language Standards

## Primary Languages

- Python
- TypeScript

Platform services use Python.

Administrative portals and web applications use TypeScript.

---

# Python Version

All backend services shall target:

```text
Python 3.13+
```

No service may support older runtime versions unless explicitly approved.

---

# Package Management

Use:

```text
uv
```

Requirements:

- Locked dependencies
- Reproducible builds
- Deterministic environments

Direct use of `pip install` for production dependency management is prohibited.

---

# Project Layout

Every service follows:

```text
src/

api/
application/
domain/
infrastructure/
integrations/
repositories/
events/
middleware/
security/
telemetry/
workers/

tests/

configs/

migrations/
```

Business logic shall never reside inside API controllers.

---

# Import Rules

Imports are ordered as follows:

1. Standard library
2. Third-party libraries
3. Shared platform packages
4. Local modules

Example:

```python
import asyncio
from pathlib import Path

from fastapi import APIRouter

from enterprise_ai.logging import get_logger

from .service import WorkflowService
```

Wildcard imports are prohibited.

---

# Naming Conventions

## Modules

```text
snake_case.py
```

---

## Packages

```text
snake_case
```

---

## Variables

```python
user_id

workflow_name

request_timeout
```

---

## Functions

Use verbs.

Good:

```python
create_workflow()

store_memory()

generate_response()
```

Avoid:

```python
workflow()

memory()

response()
```

---

## Classes

PascalCase.

```python
WorkflowEngine

MemoryRepository

PromptBuilder
```

---

## Constants

UPPER_SNAKE_CASE.

```python
DEFAULT_TIMEOUT

MAX_TOKENS

CACHE_TTL
```

---

## Private Members

Prefix with underscore.

```python
_build_prompt()

_validate_request()
```

---

# Type Hints

Mandatory.

Every public function shall define:

- Parameter types
- Return type

Example:

```python
def create_memory(
    request: MemoryRequest
) -> MemoryResponse:
    ...
```

Avoid untyped APIs.

---

# Docstrings

Use Google-style docstrings.

Example:

```python
def search(query: str) -> list[str]:
    """
    Search indexed knowledge.

    Args:
        query:
            Search query.

    Returns:
        Matching document identifiers.
    """
```

Public APIs require documentation.

---

# Async Programming

Backend services shall use asynchronous programming whenever practical.

Use:

```python
async def
```

Avoid blocking operations.

Blocking libraries must execute using worker threads or dedicated background processes.

---

# Dependency Injection

Services shall depend on abstractions rather than concrete implementations.

Example:

```python
KnowledgeService(
    repository: KnowledgeRepository
)
```

Avoid:

```python
KnowledgeService(
    PostgresKnowledgeRepository()
)
```

Object creation belongs to the composition root.

---

# Error Handling

Errors shall be:

- Explicit
- Typed
- Logged
- Actionable

Never swallow exceptions.

Bad:

```python
try:
    ...
except:
    pass
```

Good:

```python
try:
    ...
except ValidationError as ex:
    logger.warning(...)
    raise
```

---

# Custom Exceptions

Business errors require custom exception classes.

Example:

```python
KnowledgeNotFoundError

InvalidWorkflowStateError

PromptValidationError
```

Avoid generic RuntimeError for business failures.

---

# Logging

Logging shall use structured logging.

Every log entry should include:

- Timestamp
- Service
- Trace ID
- Correlation ID
- Tenant
- User (when appropriate)
- Severity

Sensitive information shall never be logged.

---

# Configuration

Configuration shall come from:

- Environment variables
- Configuration service
- Secret manager

Hardcoded configuration values are prohibited.

---

# Security

Code shall never:

- Store secrets
- Log credentials
- Disable TLS validation
- Ignore authentication
- Ignore authorization
- Trust external input

All external input must be validated.

---

# API Layer

API controllers should:

- Validate requests
- Call application services
- Return responses

Controllers shall not contain business logic.

---

# Domain Layer

Domain models contain:

- Business rules
- Validation
- State transitions

Infrastructure concerns are prohibited.

---

# Infrastructure Layer

Responsible for:

- Databases
- Message brokers
- AI providers
- External systems
- Object storage

Business rules belong elsewhere.

---

# Repository Layer

Repositories abstract persistence.

Example:

```python
MemoryRepository

KnowledgeRepository

WorkflowRepository
```

SQL should remain inside repository implementations.

---

# Testing Requirements

Every new feature requires:

- Unit tests
- Integration tests (where applicable)
- Regression tests for resolved defects

Untested code should not be merged.

---

# Code Review Standards

Reviewers shall evaluate:

- Correctness
- Readability
- Maintainability
- Security
- Performance
- Test coverage
- Documentation

Large pull requests should be avoided.

---

# Performance

Avoid:

- N+1 queries
- Blocking I/O in async code
- Excessive memory allocation
- Unbounded loops
- Inefficient serialization

Measure performance before optimizing.

---

# Comments

Code should explain **why**, not **what**.

Avoid redundant comments.

Bad:

```python
# Increment counter
counter += 1
```

Good:

```python
# Retry count is incremented to enforce exponential backoff.
counter += 1
```

---

# Formatting

Formatting shall be automated.

Recommended tools:

- Ruff
- Black (if adopted)
- isort
- mypy

Developers should not manually format code.

---

# Static Analysis

Every commit must pass:

- Ruff
- mypy
- Bandit
- Semgrep

Critical findings block merges.

---

# Documentation

Every public package shall include:

- README
- Architecture overview
- Configuration guide
- Usage examples
- Changelog

---

# AI Development

AI integrations shall:

- Validate prompts
- Validate responses
- Handle model failures
- Track token usage
- Record latency
- Capture provider metadata

Prompt templates must remain version-controlled.

---

# Prohibited Practices

The following are prohibited:

- Global mutable state
- Circular imports
- Magic numbers
- Hardcoded credentials
- Silent exception handling
- Deeply nested conditionals
- Copy-paste implementations
- Business logic inside controllers
- Business logic inside repositories
- Direct database access from APIs

---

# Code Quality Checklist

Before merging, ensure:

- Code compiles
- Tests pass
- Linting passes
- Type checking passes
- Security scans pass
- Documentation updated
- Public APIs documented
- Logging implemented
- Metrics added where required

---

# Success Criteria

The coding standards are successful when:

- Code is consistent across all services.
- Engineers can move between repositories with minimal onboarding.
- Static analysis finds few violations.
- Reviews focus on design rather than style.
- Maintenance costs decrease over time.

---

# Dependencies

- ENG-001 Engineering Foundation
- ENG-002 Repository Structure

---

# Related Documents

- ENG-004 API Standards
- ENG-005 Database Standards
- ENG-006 Event Standards
- ENG-007 Testing Strategy
- ENG-012 Secure SDLC
- ENG-016 Quality Gates

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
| Security Lead | Pending |