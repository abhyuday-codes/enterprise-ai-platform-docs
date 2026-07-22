---
title: Git Workflow
document_id: ENG-010
version: 1.0.0
status: Approved
owner: Engineering
classification: Internal
phase: Engineering
last_updated: YYYY-MM-DD
---

# Git Workflow

## Executive Summary

This document defines the Git workflow, repository governance, branching strategy, commit standards, code review process, merge policies, release management, and repository protection rules for the Enterprise AI Platform.

Version control is the foundation of engineering collaboration. Every change shall be traceable, reviewable, reproducible, and reversible.

---

# Purpose

This document defines:

- Repository governance
- Branching strategy
- Commit conventions
- Pull request workflow
- Code review standards
- Merge policies
- Release branching
- Hotfix workflow
- Repository protection
- Git best practices

---

# Git Philosophy

Git shall provide:

- Complete history
- Safe collaboration
- Controlled releases
- Reliable rollback
- Traceable changes

The repository history is a permanent engineering asset.

---

# Repository Model

The platform uses a **single modular monorepo**.

```
enterprise-ai-platform/
```

The repository contains:

- Applications
- Services
- Shared Packages
- SDKs
- Infrastructure
- Documentation
- CI/CD Pipelines

---

# Branching Strategy

The platform follows **Trunk-Based Development** with short-lived feature branches.

```
main
   │
   ├──────── feature/*
   ├──────── bugfix/*
   ├──────── hotfix/*
   ├──────── release/*
```

Feature branches shall be short-lived.

Long-running branches are discouraged.

---

# Main Branch

The `main` branch shall always be:

- Deployable
- Stable
- Protected
- Fully tested

Direct commits are prohibited.

---

# Branch Naming

## Feature

```
feature/knowledge-indexing

feature/mcp-gateway

feature/tenant-management
```

---

## Bug Fix

```
bugfix/vector-search-timeout

bugfix/token-calculation
```

---

## Hotfix

```
hotfix/security-patch

hotfix/production-outage
```

---

## Release

```
release/v1.2.0

release/v2.0.0
```

---

# Branch Lifetime

Feature branches should exist only until the associated work is completed.

Recommended duration:

- Small feature: 1–3 days
- Medium feature: < 1 week
- Large initiative: Split into multiple branches

---

# Commit Philosophy

Each commit shall represent one logical change.

Commits shall be:

- Atomic
- Reviewable
- Reversible
- Buildable

---

# Commit Message Convention

The platform adopts the Conventional Commits specification.

Format:

```
<type>(scope): <summary>
```

Examples:

```
feat(api): add workflow execution endpoint

fix(memory): resolve vector index issue

docs(architecture): update deployment diagram

refactor(events): simplify event publisher

test(search): add integration tests

ci(build): improve pipeline caching
```

---

# Allowed Commit Types

- feat
- fix
- docs
- refactor
- test
- chore
- build
- ci
- perf
- style
- revert

---

# Commit Requirements

Every commit shall:

- Compile successfully
- Pass local validation
- Include related tests (where applicable)
- Avoid unrelated changes

---

# Pull Requests

All changes shall be merged through Pull Requests.

Direct pushes to protected branches are prohibited.

---

# Pull Request Requirements

Every Pull Request shall include:

- Purpose
- Summary of changes
- Related issue or ADR
- Testing evidence
- Breaking change assessment
- Documentation updates
- Screenshots (when applicable)

---

# Pull Request Size

Recommended limits:

| Metric | Target |
|---------|--------|
| Files Changed | < 20 |
| Lines Changed | < 500 |
| Review Time | < 30 minutes |

Large changes shall be split into smaller PRs where practical.

---

# Code Review

Every Pull Request requires review.

Reviewers shall evaluate:

- Correctness
- Architecture
- Maintainability
- Security
- Performance
- Test quality
- Documentation

Style discussions should be minimized through automation.

---

# Required Approvals

Minimum approvals:

| Change Type | Approvals |
|--------------|----------:|
| Documentation | 1 |
| Application Code | 2 |
| Shared Packages | 2 |
| Infrastructure | 2 |
| Security | Security Team |
| Architecture | Architecture Team |

---

# Merge Strategy

Preferred merge strategy:

**Squash and Merge**

Benefits:

- Cleaner history
- One logical change per PR
- Easier rollback

Merge commits are reserved for release branches.

---

# Merge Requirements

A Pull Request shall not merge unless:

- CI passes
- Required approvals obtained
- Security scans succeed
- Documentation updated
- No unresolved conversations
- Branch up to date

---

# Release Branches

Release branches stabilize upcoming releases.

Example:

```
release/v2.1.0
```

Only:

- Bug fixes
- Documentation
- Release preparation

are permitted after branch creation.

---

# Hotfix Workflow

Critical production defects follow:

```
main

↓

hotfix/security-patch

↓

Validation

↓

Review

↓

Merge

↓

Production Release
```

Hotfixes shall be backported if necessary.

---

# Reverts

Reverts are preferred over force fixes.

Use:

```
git revert
```

History shall remain intact.

---

# Protected Branches

Protected branches include:

- main
- release/*

Protection rules:

- No force push
- No deletion
- Required reviews
- Required status checks
- Signed commits (recommended)

---

# Tags

Every release shall be tagged.

Format:

```
v1.0.0

v2.3.1
```

Tags are immutable.

---

# Repository Protection

Mandatory protections:

- Branch protection
- Required CI
- Required approvals
- Secret scanning
- Dependency scanning
- Signed commits (recommended)

---

# Large Files

Source repositories shall not contain:

- Build artifacts
- Generated binaries
- Large datasets
- Model weights
- Database backups

Use:

- Object Storage
- Artifact Repository
- Git LFS (approved cases)

---

# Binary Files

Binary assets shall be minimized.

Generated artifacts belong in release pipelines, not source control.

---

# Documentation Workflow

Documentation changes follow the same review process as code.

Architecture documents require architecture approval.

---

# Infrastructure Workflow

Infrastructure changes require:

- Plan review
- Security review
- Cost assessment
- Rollback plan

Infrastructure changes shall be applied through Infrastructure as Code only.

---

# Repository Automation

Automated workflows include:

- Linting
- Testing
- Security scanning
- Dependency validation
- Documentation validation
- Release generation

---

# Repository Metrics

Track:

- PR cycle time
- Review duration
- Merge frequency
- Deployment frequency
- Change failure rate
- Mean Time to Recovery (MTTR)

These metrics support engineering performance improvement.

---

# Governance

Repository administrators shall periodically review:

- Branch protections
- Access permissions
- Repository health
- Secret exposure
- Inactive branches

Access shall follow the principle of least privilege.

---

# Prohibited Practices

The following are prohibited:

- Direct commits to `main`
- Force pushes to protected branches
- Merging failing builds
- Large unrelated commits
- Skipping reviews
- Untracked release changes
- Committing secrets
- Committing generated artifacts

---

# Success Criteria

The Git workflow is successful when:

- Every change is traceable.
- Repository history remains clean.
- Releases are predictable.
- Rollbacks are reliable.
- Collaboration scales effectively.
- Repository governance is consistently enforced.

---

# Dependencies

- ENG-001 Engineering Foundation
- ENG-002 Repository Structure
- ENG-003 Coding Standards
- ENG-009 Testing Strategy

---

# Related Documents

- ENG-011 Release & Versioning
- ENG-012 CI/CD Standards
- ENG-013 Secure SDLC
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
| DevOps Lead | Approved |
| Security Lead | Pending |