---
title: API Specification Template
template_id: TEMPLATE-004
version: 1.0.0
status: Approved
owner: Platform Architecture Team
classification: Internal
last_updated: YYYY-MM-DD
---

# {{ API Name }}

## Executive Summary

Provide a concise overview of the API.

Summarize:

- Purpose
- Primary consumers
- Business capabilities
- Authentication requirements

---

# Purpose

Describe why this API exists.

Include:

- Business objectives
- Platform responsibilities
- Expected consumers
- Problems solved

---

# Scope

### In Scope

- REST endpoints
- Request/response contracts
- Authentication
- Authorization
- Error handling
- Versioning

### Out of Scope

- Internal implementation
- UI behavior
- Deployment configuration

---

# API Overview

| Property | Value |
|----------|-------|
| API Name | {{ API Name }} |
| Base URL | `/api/v1/...` |
| Version | v1 |
| Protocol | HTTPS |
| Format | JSON |
| Authentication | OAuth2 / JWT |
| Authorization | RBAC / ABAC |

---

# Consumers

List intended consumers.

Examples:

- Web Portal
- Cursor Extension
- VS Code Extension
- CLI
- SDK
- Internal Services
- Third-Party Integrations

---

# Authentication

Describe authentication requirements.

Supported mechanisms:

- OAuth 2.0
- OpenID Connect
- JWT Bearer Token
- API Keys (if applicable)
- Managed Identity

Example:

```http
Authorization: Bearer <access_token>
```

---

# Authorization

Document authorization rules.

Example:

| Role | Permissions |
|------|-------------|
| Administrator | Full Access |
| Developer | Read / Write |
| Viewer | Read Only |

Include ABAC policies where applicable.

---

# API Versioning

Document the versioning strategy.

Example:

```text
/api/v1/
/api/v2/
```

Rules:

- Breaking changes require a new major version.
- Backward-compatible additions increment the minor version.
- Deprecated versions should have a defined retirement policy.

---

# Endpoints

## Endpoint Template

### {{ Endpoint Name }}

**Method**

```http
GET
```

**Path**

```text
/api/v1/resource
```

**Description**

Describe the purpose of the endpoint.

---

### Request Headers

| Header | Required | Description |
|---------|----------|-------------|
| Authorization | Yes | Bearer token |
| Content-Type | Yes | application/json |
| Correlation-Id | Recommended | Distributed tracing |

---

### Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| id | UUID | Resource identifier |

---

### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| page | Integer | No | Page number |
| pageSize | Integer | No | Page size |

---

### Request Body

```json
{
  "property": "value"
}
```

---

### Successful Response

**Status Code**

```http
200 OK
```

**Response**

```json
{
  "id": "uuid",
  "name": "example"
}
```

---

### Error Responses

| Status | Description |
|---------|-------------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

---

# Data Models

Document request and response models.

## Example Request

```json
{
  "name": "example"
}
```

## Example Response

```json
{
  "id": "uuid",
  "name": "example",
  "createdAt": "2026-01-01T00:00:00Z"
}
```

---

# Validation Rules

Document validation requirements.

Example:

| Field | Rule |
|------|------|
| Name | Required |
| Email | RFC 5322 |
| ID | UUID v4 |
| Limit | 1–100 |

---

# Error Model

Define the standard error response.

```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "The requested resource was not found.",
    "correlationId": "uuid",
    "timestamp": "2026-01-01T00:00:00Z"
  }
}
```

---

# Pagination

If applicable, document pagination.

Example:

```http
GET /api/v1/resources?page=1&pageSize=20
```

Response:

```json
{
  "page": 1,
  "pageSize": 20,
  "totalItems": 100,
  "totalPages": 5,
  "items": []
}
```

---

# Filtering

Example:

```http
GET /api/v1/resources?status=active
```

---

# Sorting

Example:

```http
GET /api/v1/resources?sort=name,-createdAt
```

---

# Rate Limiting

Document API limits.

Example:

| Consumer | Limit |
|----------|-------|
| Authenticated User | 1,000 requests/hour |
| Service Account | Configurable |

Document response headers if applicable.

---

# Idempotency

Document support for idempotent operations.

Example:

```http
Idempotency-Key: <uuid>
```

Applicable to:

- POST
- PUT
- PATCH

where retry safety is required.

---

# Security Considerations

Document API security.

Include:

- Input validation
- Output encoding
- Authentication
- Authorization
- Rate limiting
- Audit logging
- Encryption in transit
- Sensitive data masking

---

# Observability

Document telemetry.

Include:

- Correlation IDs
- Request logging
- Metrics
- Distributed tracing
- Audit events

---

# Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| Availability | TBD |
| Performance | TBD |
| Latency | TBD |
| Security | TBD |
| Reliability | TBD |

---

# OpenAPI Specification

Reference the OpenAPI document.

Example:

```text
openapi/api-name.yaml
```

---

# SDK Support

Document available SDKs.

| Language | Status |
|----------|--------|
| Python | Planned |
| TypeScript | Planned |
| C# | Planned |

---

# Deprecation Policy

Document API lifecycle.

Stages:

1. Active
2. Deprecated
3. End-of-Life
4. Removed

Provide migration guidance for deprecated APIs.

---

# Related Documents

- `../documentation-standards.md`
- `../03-architecture/`
- `../04-engineering/`
- `../api/`

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0.0 | YYYY-MM-DD | Author | Initial version |

---

# Approval

| Role | Name | Status |
|------|------|--------|
| API Owner | TBD | Pending |
| Solution Architect | TBD | Pending |
| Engineering Lead | TBD | Pending |
| Security Architect | TBD | Pending |
| Platform Owner | TBD | Pending |
