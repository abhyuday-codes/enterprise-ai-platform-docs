---
title: Architecture Decision Record (ADR) Template
template_id: TEMPLATE-005
version: 1.0.0
status: Approved
owner: Platform Architecture Team
classification: Internal
last_updated: YYYY-MM-DD
---

# ADR-{{ Number }}: {{ Decision Title }}

## Status

> Proposed | Accepted | Superseded | Deprecated | Rejected

---

# Executive Summary

Provide a brief summary of the architectural decision.

Summarize:

- What decision is being made
- Why it is important
- Expected impact on the platform

This section should be understandable without reading the remainder of the document.

---

# Decision Metadata

| Property | Value |
|----------|-------|
| ADR Number | ADR-{{ Number }} |
| Title | {{ Decision Title }} |
| Status | Proposed |
| Date | YYYY-MM-DD |
| Decision Owner | TBD |
| Reviewers | TBD |
| Supersedes | None |
| Superseded By | None |

---

# Context

Describe the situation that requires this decision.

Include:

- Business context
- Technical context
- Existing architecture
- Current limitations
- Relevant constraints
- Stakeholder concerns

Readers should understand why a decision is necessary.

---

# Problem Statement

Clearly define the problem.

Answer questions such as:

- What issue are we solving?
- Why is it important?
- What happens if no decision is made?

---

# Decision Drivers

List the factors influencing the decision.

Examples:

- Scalability
- Performance
- Security
- Cost
- Reliability
- Compliance
- Maintainability
- Developer Experience
- Operational Complexity
- Time to Market

---

# Considered Options

Document every viable option that was evaluated.

| Option | Description |
|---------|-------------|
| Option A | Description |
| Option B | Description |
| Option C | Description |

---

# Option Analysis

## Option A

### Description

Describe the option.

### Advantages

- Advantage
- Advantage

### Disadvantages

- Disadvantage
- Disadvantage

---

## Option B

### Description

Describe the option.

### Advantages

- Advantage
- Advantage

### Disadvantages

- Disadvantage
- Disadvantage

---

## Option C

### Description

Describe the option.

### Advantages

- Advantage
- Advantage

### Disadvantages

- Disadvantage
- Disadvantage

---

# Decision

State the selected option.

Clearly explain:

- Which option was selected
- Why it was selected
- Why other options were rejected

This should be the authoritative architectural decision.

---

# Rationale

Explain the reasoning behind the decision.

Discuss:

- Technical reasoning
- Business reasoning
- Trade-offs accepted
- Long-term considerations

---

# Consequences

Describe the impact of the decision.

## Positive

- Benefit
- Benefit
- Benefit

## Negative

- Drawback
- Drawback

## Neutral

- Observation
- Observation

---

# Implementation Guidance

Provide implementation recommendations.

Examples:

- Required technologies
- Design patterns
- Coding standards
- Migration strategy
- Deployment considerations

---

# Risks

Identify risks introduced by this decision.

| Risk | Impact | Mitigation |
|------|--------|------------|
| Risk | High | Mitigation |

---

# Assumptions

Document assumptions.

Examples:

- Kubernetes remains the deployment platform.
- gRPC is available for internal communication.
- Azure is the primary cloud provider.

---

# Dependencies

List related dependencies.

Examples:

- API Gateway
- Event Bus
- Identity Provider
- Kubernetes
- PostgreSQL

---

# Alternatives for Future Review

Capture alternatives that may become viable later.

Examples:

- Technology upgrades
- Cloud-native alternatives
- Open-source replacements

---

# Review Criteria

Describe conditions that should trigger a review.

Examples:

- Significant scale increase
- New compliance requirements
- Platform migration
- Cost increases
- Vendor lock-in concerns

---

# Related Decisions

Reference other ADRs.

Examples:

- ADR-001 — API Communication Strategy
- ADR-002 — Authentication Strategy
- ADR-003 — Event Bus Selection

---

# Related Documents

- `../documentation-standards.md`
- `../03-architecture/`
- `../04-engineering/`
- `../05-platform/`

---

# References

Include any supporting references.

Examples:

- RFCs
- Vendor documentation
- Design documents
- Proof of Concepts
- Benchmark reports

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0.0 | YYYY-MM-DD | Author | Initial version |

---

# Approval

| Role | Name | Status |
|------|------|--------|
| Enterprise Architect | TBD | Pending |
| Solution Architect | TBD | Pending |
| Engineering Lead | TBD | Pending |
| Security Architect | TBD | Pending |
| Platform Owner | TBD | Pending |
