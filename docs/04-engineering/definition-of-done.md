---
title: Definition of Done
document_id: ENG-015
version: 1.0.0
status: Approved
owner: Engineering
classification: Internal
phase: Engineering
last_updated: YYYY-MM-DD
---

# Definition of Done

## Executive Summary

This document defines the mandatory completion criteria for all engineering work within the Enterprise AI Platform.

No user story, task, service, package, infrastructure component, AI capability, or documentation effort shall be considered complete until every applicable criterion in this document has been satisfied.

The Definition of Done (DoD) provides a consistent quality baseline across all engineering teams and prevents incomplete work from progressing through the delivery pipeline.

---

# Purpose

This document defines completion criteria for:

- Features
- Bug fixes
- Services
- APIs
- Infrastructure
- AI capabilities
- Documentation
- Security
- Testing
- Deployment
- Operations

---

# Engineering Philosophy

Completion means more than code.

A work item is complete only when it is:

- Correct
- Tested
- Secure
- Observable
- Documented
- Deployable
- Maintainable
- Governed

---

# General Definition of Done

Every work item shall satisfy the following:

- Requirements implemented
- Acceptance criteria met
- Code reviewed
- Tests passing
- Documentation updated
- Security validated
- CI/CD successful
- Quality Gates passed
- Ready for production

---

# Requirements

Before completion:

- Functional requirements implemented
- Non-functional requirements addressed
- Edge cases considered
- Error scenarios handled

No known acceptance criteria may remain incomplete.

---

# Architecture

The implementation shall:

- Follow approved architecture
- Respect service boundaries
- Follow dependency rules
- Avoid unnecessary coupling

Architecture deviations require an approved ADR.

---

# Coding Standards

Implementation shall comply with:

- Coding Standards
- API Standards
- Database Standards
- Event Standards
- Configuration Standards

Static analysis shall report no blocking issues.

---

# Testing Requirements

Mandatory:

- Unit tests
- Integration tests
- Contract tests
- Regression tests

Where applicable:

- Performance tests
- Security tests
- End-to-end tests
- Chaos tests

All mandatory tests shall pass.

---

# Code Coverage

Minimum expectations:

| Area | Requirement |
|------|------------:|
| Business Logic | ≥ 80% |
| Critical Services | ≥ 90% |
| API Contracts | 100% |
| Event Contracts | 100% |

Coverage shall be meaningful rather than artificially inflated.

---

# Security

Before completion:

- No critical vulnerabilities
- Secrets protected
- Authentication verified
- Authorization verified
- Dependency scan passed
- Container scan passed

Security exceptions require formal approval.

---

# AI Requirements

Applicable to AI-enabled components.

Mandatory:

- Prompt versioned
- Prompt evaluated
- Model approved
- AI evaluation passed
- Hallucination assessment completed
- Safety validation completed
- Cost impact assessed

Prompt changes require regression evaluation.

---

# RAG Requirements

Knowledge systems shall verify:

- Chunk quality
- Retrieval accuracy
- Citation quality
- Embedding validation
- Index health

Knowledge updates shall be reproducible.

---

# MCP Requirements

MCP implementations shall:

- Publish schemas
- Validate requests
- Validate responses
- Enforce permissions
- Emit telemetry
- Produce audit logs

---

# Documentation

Documentation shall include:

- Purpose
- Architecture
- Configuration
- APIs
- Events
- Dependencies
- Operational guidance

Documentation shall be updated before merge.

---

# Observability

Every deployable component shall provide:

- Structured logs
- Metrics
- Distributed tracing
- Correlation IDs
- Health endpoints
- Readiness checks

Operational visibility is mandatory.

---

# Configuration

Configuration shall be:

- Externalized
- Validated
- Environment-aware
- Documented

Secrets shall never be stored in source control.

---

# Deployment Readiness

Deployment shall support:

- Automated deployment
- Rollback
- Health validation
- Version tracking

Manual deployment steps shall not be required.

---

# Operational Readiness

Operational documentation shall include:

- Runbook
- Monitoring
- Alerting
- Recovery procedures
- Escalation path

Critical services require documented disaster recovery procedures.

---

# Accessibility

User-facing applications shall meet applicable accessibility standards.

Accessibility regressions shall block release.

---

# Performance

Performance requirements shall be validated.

Applicable checks include:

- Response time
- Throughput
- Resource utilization
- Scalability

Performance regressions require investigation.

---

# Compliance

Applicable regulatory requirements shall be satisfied.

Examples include:

- GDPR
- SOC 2
- ISO 27001
- HIPAA (deployment specific)

Compliance evidence shall be retained where required.

---

# Code Review

Every Pull Request shall:

- Receive required approvals
- Resolve review comments
- Pass automated validation

No unresolved blocking comments may remain.

---

# CI/CD

The pipeline shall complete successfully.

Mandatory stages:

- Build
- Test
- Security Scan
- Artifact Generation
- Documentation Validation

Production artifacts shall be signed.

---

# Release Readiness

Before release:

- Release notes updated
- Version assigned
- Migration guide prepared (if applicable)
- Rollback procedure documented

---

# Defect Resolution

Every resolved defect shall include:

- Root cause identified
- Regression test added
- Documentation updated (if required)

Recurring issues require engineering review.

---

# Metrics

Engineering teams shall monitor:

- Defect escape rate
- Deployment success
- Lead time
- MTTR
- AI evaluation score
- Test coverage

Metrics shall drive continuous improvement.

---

# Team Responsibilities

## Developer

Responsible for:

- Implementation
- Testing
- Documentation
- Local validation

---

## Reviewer

Responsible for:

- Correctness
- Maintainability
- Architecture
- Security

---

## QA

Responsible for:

- Validation
- Acceptance testing
- Regression verification

---

## DevOps

Responsible for:

- Pipeline health
- Deployment readiness
- Artifact management

---

## Security

Responsible for:

- Security review
- Vulnerability assessment
- Risk acceptance

---

# Governance

No work item shall transition to "Done" unless:

- Definition of Done satisfied
- Quality Gates passed
- Required approvals obtained

Exceptions require documented approval from Engineering leadership.

---

# Checklist

Every work item shall satisfy:

- [ ] Requirements complete
- [ ] Architecture compliant
- [ ] Code reviewed
- [ ] Tests passing
- [ ] Coverage targets achieved
- [ ] Security validated
- [ ] Documentation updated
- [ ] Observability implemented
- [ ] Deployment validated
- [ ] Operational documentation completed
- [ ] CI/CD passed
- [ ] Release ready

---

# Prohibited Practices

The following are prohibited:

- Marking incomplete work as Done
- Skipping required tests
- Ignoring security findings
- Merging undocumented features
- Deploying without observability
- Releasing without rollback capability
- Closing defects without regression tests

---

# Success Criteria

The Definition of Done is successful when:

- Engineering quality is consistent.
- Releases are production-ready.
- Technical debt is minimized.
- Security and compliance are maintained.
- Operational readiness is achieved before deployment.
- Teams share a common understanding of completion.

---

# Dependencies

- ENG-003 Coding Standards
- ENG-009 Testing Strategy
- ENG-010 Git Workflow
- ENG-011 Release & Versioning
- ENG-012 CI/CD Standards
- ENG-013 Secure SDLC
- ENG-014 AI Development Standards

---

# Related Documents

- ENG-016 Quality Gates
- Engineering Foundation
- Security Architecture
- Observability Architecture

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
| QA Lead | Approved |
| Security Lead | Approved |
| Platform Operations | Approved |