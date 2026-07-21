---
title: Service Design Template
template_id: TEMPLATE-003
version: 1.0.0
status: Approved
owner: Platform Architecture Team
classification: Internal
last_updated: YYYY-MM-DD
---

# {{ Service Name }}

## Executive Summary

Provide a concise overview of the service.

Summarize:

- Business purpose
- Responsibilities
- Position within the platform
- Key capabilities

This section should provide enough context for readers before diving into implementation details.

---

# Purpose

Describe why this service exists.

Include:

- Business problem solved
- Technical purpose
- Platform responsibilities
- Expected outcomes

---

# Scope

### In Scope

- Responsibilities owned by this service
- Supported APIs
- Data ownership
- Event publishing and consumption

### Out of Scope

- Responsibilities of other services
- Infrastructure deployment
- UI implementation
- Client-specific behavior

---

# Background

Provide context behind the creation of the service.

Examples:

- Business drivers
- Technical requirements
- Existing limitations
- Previous implementation

---

# Service Overview

Describe the service at a high level.

Include:

- Responsibilities
- Dependencies
- Consumers
- Upstream systems
- Downstream systems

---

# Responsibilities

List everything this service owns.

Example:

- Validate requests
- Execute business logic
- Store metadata
- Publish domain events
- Maintain audit records

---

# Non-Responsibilities

Clearly state what this service should never do.

Example:

- User authentication
- Infrastructure provisioning
- Direct UI rendering
- Cross-domain business logic

---

# Architecture Overview

Describe how the service fits into the overall platform.

Topics may include:

- Internal modules
- Layered architecture
- Clean Architecture
- Hexagonal Architecture
- Domain-Driven Design (DDD)

> Include architecture diagram if applicable.

---

# Service Interfaces

Document all interfaces exposed by the service.

| Interface | Technology | Purpose |
|-----------|------------|---------|
| REST API | HTTP | External access |
| gRPC | Protocol Buffers | Internal communication |
| Events | Kafka / Azure Service Bus | Asynchronous messaging |

---

# API Endpoints

Document REST endpoints.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/resource` | Retrieve resources |
| POST | `/resource` | Create resource |
| PUT | `/resource/{id}` | Update resource |
| DELETE | `/resource/{id}` | Delete resource |

---

# gRPC Contracts

Document internal gRPC services.

| Service | Method | Purpose |
|----------|--------|---------|
| ExampleService | GetItem | Retrieve data |

Reference the corresponding `.proto` files when available.

---

# Event Contracts

## Events Published

| Event | Description |
|--------|-------------|
| ResourceCreated | Resource successfully created |
| ResourceUpdated | Resource updated |

## Events Consumed

| Event | Purpose |
|--------|----------|
| UserCreated | Initialize service data |
| PolicyUpdated | Refresh policies |

---

# Data Model

Describe the data owned by the service.

## Primary Entities

| Entity | Description |
|---------|-------------|
| Entity | Description |

Include:

- Relationships
- Ownership
- Lifecycle

---

# Database Design

Describe persistent storage.

| Storage | Purpose |
|---------|----------|
| PostgreSQL | Transactional data |
| Redis | Cache |
| ChromaDB | Embeddings |
| Blob Storage | Documents |

---

# Cache Strategy

Describe caching behavior.

Include:

- Cache type
- Expiration
- Cache invalidation
- Distributed caching

Example:

- Redis
- Semantic Cache
- Response Cache
- Metadata Cache

---

# Security

Document service security.

Include:

- Authentication
- Authorization
- RBAC
- ABAC
- Secret management
- Encryption
- Input validation
- Output sanitization

---

# Configuration

Document configurable settings.

| Setting | Description | Default |
|----------|-------------|---------|
| Example | Description | Value |

---

# Error Handling

Describe failure handling.

Include:

- Validation errors
- Business errors
- Retry behavior
- Circuit breakers
- Timeouts
- Dead-letter queues

---

# Observability

Document monitoring strategy.

## Metrics

Examples:

- Request count
- Latency
- Throughput
- Error rate

## Logging

Include:

- Structured logging
- Correlation IDs
- Sensitive data handling

## Distributed Tracing

Include:

- Trace propagation
- OpenTelemetry
- Span naming

---

# Performance Considerations

Document performance expectations.

Examples:

- Response time targets
- Throughput
- Concurrent requests
- Batch processing

---

# Scalability Strategy

Describe scaling behavior.

Examples:

- Stateless service
- Horizontal Pod Autoscaler
- Resource limits
- Partitioning
- Event-driven scaling

---

# High Availability

Describe resilience strategy.

Examples:

- Multiple replicas
- Health checks
- Readiness probes
- Liveness probes
- Graceful shutdown

---

# Dependencies

Document upstream and downstream dependencies.

## Upstream Services

| Service | Purpose |
|----------|----------|
| API Gateway | Client requests |

## Downstream Services

| Service | Purpose |
|----------|----------|
| Knowledge Service | Retrieve knowledge |
| Audit Service | Persist audit logs |

---

# Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| Availability | TBD |
| Reliability | TBD |
| Scalability | TBD |
| Performance | TBD |
| Security | TBD |
| Maintainability | TBD |

---

# Assumptions

Document assumptions.

Examples:

- Authentication is handled by the API Gateway.
- Database connectivity is highly available.
- Event Bus guarantees at-least-once delivery.

---

# Constraints

Document technical or business constraints.

Examples:

- Regulatory compliance
- Budget
- Technology stack
- Latency requirements

---

# Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Risk | High | Mitigation |

---

# Testing Strategy

Document testing requirements.

Include:

- Unit tests
- Integration tests
- Contract tests
- Load tests
- Security tests
- Chaos testing
- Performance testing

---

# Deployment Considerations

Document deployment requirements.

Include:

- Docker image
- Kubernetes deployment
- Helm chart
- Resource requests
- Resource limits
- Secrets
- ConfigMaps

---

# Operational Runbook

Document operational guidance.

Include:

- Startup procedure
- Shutdown procedure
- Health checks
- Common failures
- Recovery steps

---

# Future Enhancements

Capture planned improvements.

Examples:

- Additional APIs
- Improved caching
- AI enhancements
- Performance optimization

---

# Related Documents

- `../documentation-standards.md`
- `../03-architecture/`
- `../api/`
- `../09-decisions/`

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0.0 | YYYY-MM-DD | Author | Initial version |

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Service Owner | TBD | Pending |
| Solution Architect | TBD | Pending |
| Engineering Lead | TBD | Pending |
| Security Architect | TBD | Pending |
| Platform Owner | TBD | Pending |
