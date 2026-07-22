---
title: Database Standards
document_id: ENG-005
version: 1.0.0
status: Approved
owner: Engineering
classification: Internal
phase: Engineering
last_updated: YYYY-MM-DD
---

# Database Standards

## Executive Summary

This document defines the engineering standards for data persistence within the Enterprise AI Platform. The platform adopts the **Database-per-Service** architectural pattern to ensure service autonomy, scalability, security, and operational independence.

Every service owns its data, schema, migrations, indexes, and lifecycle. Cross-service database access is prohibited.

---

# Purpose

This document defines:

- Database architecture
- Database ownership
- Database technology
- Data modeling
- Naming conventions
- Constraints
- Transactions
- Migrations
- Indexing
- Performance
- Multi-tenancy
- Auditing
- Data retention
- Backup & recovery
- Database governance

---

# Database Philosophy

The platform follows these principles:

- Database per Service
- Domain ownership
- Strong consistency where required
- Eventual consistency between services
- Schema evolution
- Secure by default
- Observable by default
- Automated migrations

Databases are implementation details of services and shall never be exposed directly.

---

# Supported Technologies

Primary Relational Database

- PostgreSQL

Supporting Technologies

- pgvector
- Redis
- OpenSearch
- ChromaDB (specialized AI workloads)
- Object Storage

Each technology shall be used only for its intended purpose.

---

# Database Ownership

Each service owns:

- Database
- Schema
- Tables
- Views
- Indexes
- Constraints
- Migrations
- Stored procedures (if approved)

Examples:

```text
Knowledge Service
    ↓
knowledge_db

Memory Service
    ↓
memory_db

Workflow Service
    ↓
workflow_db
```

No other service may access these databases directly.

---

# Communication Between Services

Services communicate using:

- REST APIs
- gRPC
- Kafka Events

Never through SQL queries.

Example:

```text
Service A

    SQL

Service B
```

❌ Prohibited

Instead:

```text
Service A

 REST/gRPC/Event

Service B
```

✅ Required

---

# Schema Design Principles

Schemas shall be:

- Simple
- Normalized where practical
- Explicit
- Versioned
- Backward compatible
- Well documented

Avoid premature optimization.

---

# Normalization

Preferred:

Third Normal Form (3NF)

Denormalization is allowed only when justified by:

- Performance
- Analytics
- Search optimization

Such decisions require architectural approval.

---

# Naming Conventions

## Database

```text
knowledge_db

memory_db

workflow_db
```

---

## Schemas

Use snake_case.

Example:

```text
public

audit

internal
```

---

## Tables

Plural nouns.

Examples:

```text
documents

workflows

workflow_runs

users

permissions
```

---

## Columns

snake_case.

Examples:

```text
created_at

updated_at

tenant_id

workflow_name
```

---

## Primary Keys

Use:

```text
id UUID
```

UUID v7 is preferred for improved index locality.

Auto-increment integer keys are discouraged for distributed systems.

---

# Foreign Keys

Foreign keys shall only reference tables within the same service database.

Cross-service foreign keys are prohibited.

---

# Common Columns

Every business table should include:

```text
id

tenant_id

created_at

created_by

updated_at

updated_by

version
```

Soft-deletable entities should additionally include:

```text
deleted_at

deleted_by
```

---

# Data Types

Preferred types:

| Data | Type |
|------|------|
| Identifier | UUID |
| Timestamp | TIMESTAMPTZ |
| Money | NUMERIC |
| Boolean | BOOLEAN |
| JSON | JSONB |
| Binary | BYTEA |

Use the most restrictive type that satisfies the business requirement.

---

# JSON Usage

JSONB is appropriate for:

- AI metadata
- Model responses
- Dynamic configuration
- Extensible attributes

Business-critical relational data should not be stored exclusively in JSON.

---

# Constraints

Every table shall define:

- Primary Key
- Required constraints
- Unique constraints
- Check constraints where applicable

Example:

```sql
CHECK(token_count >= 0)
```

Constraints enforce business invariants whenever possible.

---

# Indexing

Indexes shall be created for:

- Foreign keys
- Frequently filtered columns
- Frequently sorted columns
- Tenant identifiers
- Search columns

Avoid unnecessary indexes that degrade write performance.

---

# Composite Indexes

Composite indexes should reflect common query patterns.

Example:

```text
tenant_id

created_at
```

---

# Transactions

Transactions shall be:

- Short-lived
- Explicit
- Atomic

Avoid long-running transactions.

Distributed transactions are prohibited.

Use Saga patterns for cross-service consistency.

---

# Concurrency Control

Preferred mechanisms:

- Optimistic locking
- Version columns
- Retry strategies

Pessimistic locking shall be limited to exceptional cases.

---

# Migrations

Schema changes shall use:

Alembic

Every migration shall be:

- Version controlled
- Reversible where practical
- Reviewed
- Tested

Manual production schema changes are prohibited.

---

# Migration Rules

Each migration shall:

- Contain one logical change
- Preserve backward compatibility
- Avoid destructive changes during deployment
- Support zero-downtime deployments

---

# Soft Deletes

Soft deletion is preferred for business entities.

Use:

```text
deleted_at

deleted_by
```

Hard deletes require explicit approval or legal justification.

---

# Auditing

Critical entities shall record:

- Creation
- Modification
- Deletion
- User
- Timestamp
- Tenant

Audit records shall be immutable.

---

# Multi-Tenancy

Every tenant-aware table shall include:

```text
tenant_id
```

Queries shall always scope data by tenant.

Cross-tenant access is prohibited.

---

# Encryption

Sensitive data shall be encrypted:

At Rest

- Database encryption
- Storage encryption

In Transit

- TLS
- mTLS where applicable

Application-level encryption shall be used for highly sensitive fields.

---

# Secrets

Secrets shall never be stored in application tables.

Use:

- Azure Key Vault
- HashiCorp Vault
- Approved secret manager

---

# Performance Standards

Databases shall be monitored for:

- Query latency
- Connection usage
- Lock contention
- Deadlocks
- Cache hit ratio
- Index efficiency

Slow queries shall be investigated continuously.

---

# Query Standards

Prefer:

- Explicit column selection
- Parameterized queries
- Repository abstraction
- Pagination

Avoid:

```sql
SELECT *
```

Production queries should retrieve only required columns.

---

# Repository Pattern

Database access shall occur only through repository implementations.

Example:

```text
KnowledgeRepository

WorkflowRepository

MemoryRepository
```

Direct SQL inside controllers or services is prohibited.

---

# Vector Data

Vector embeddings shall be stored using:

- pgvector
- ChromaDB (approved workloads)

Embedding dimensions shall remain consistent within an index.

---

# Search Data

Full-text search indexes belong in OpenSearch.

Avoid using PostgreSQL as a replacement for enterprise search.

---

# Backup Strategy

Databases shall support:

- Automated backups
- Point-in-Time Recovery (PITR)
- Backup verification
- Encryption

Recovery procedures shall be tested regularly.

---

# Retention Policy

Retention periods shall comply with:

- Business requirements
- Customer contracts
- Regulatory requirements

Expired data shall be removed using approved retention workflows.

---

# Monitoring

Database observability shall include:

- Availability
- Query duration
- Active sessions
- Replication health
- Storage usage
- Failed transactions
- Deadlocks
- Migration history

Metrics shall integrate with the platform observability stack.

---

# Database Governance

Schema modifications require:

- Design review
- Migration review
- Performance assessment
- Security review
- Backward compatibility validation

Breaking schema changes require an ADR.

---

# Prohibited Practices

The following are prohibited:

- Shared databases
- Cross-service SQL access
- Manual production schema changes
- Unbounded queries
- SELECT *
- Hardcoded SQL credentials
- Missing indexes on high-volume queries
- Long-running transactions
- Business logic in stored procedures (unless explicitly approved)

---

# Success Criteria

Database standards are successful when:

- Every service independently manages its data.
- Schema evolution is predictable and safe.
- Migrations are automated and repeatable.
- Cross-service coupling is minimized.
- Database performance remains measurable.
- Data governance is consistently enforced.

---

# Dependencies

- ENG-001 Engineering Foundation
- ENG-002 Repository Structure
- ENG-003 Coding Standards
- ENG-004 API Standards
- Data Architecture
- Multi-Tenancy Architecture

---

# Related Documents

- ENG-006 Event Standards
- ENG-007 Testing Strategy
- Security Architecture
- Data Architecture
- Resilience & Reliability Architecture

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
| Database Architect | Pending |