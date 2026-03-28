# Decision Log

| ID | Category | Title |
| :--- | :--- | :--- |
| [ADR-0001](./0001-programmatic-maintenance-state.md) | Standards | [Programmatic Maintenance State for Infrastructure](./0001-programmatic-maintenance-state.md) |
| [ADR-0002](./0002-unified-configuration-source-of-truth.md) | Standards | [Unified Configuration Source of Truth](./0002-unified-configuration-source-of-truth.md) |
| [ADR-0003](./0003-kafka-node-id-convention.md) | Conventions | [Kafka node ID Convention](./0003-kafka-node-id-convention.md) |
| [ADR-0004](./0004-disaster-recovery-strategy.md) | Strategies | [Disaster Recovery Strategy and RPO/RTO Targets](./0004-disaster-recovery-strategy.md) |
| [ADR-0005](./0005-problem-first-decision-validation.md) | Strategies | [Problem-First Decision Validation](./0005-problem-first-decision-validation.md) |

# Categories
All ADRs are divided into three categories to avoid the chaos and to not over-engineer the hierarchy:
* **Strategies** - The "Big Picture" and Governance. *(The Why)*
* **Standards** - Global technical patterns and architecture. *(The How)*
* **Conventions** - Implementation specifics and naming schemas. *(The What)*. Ensures the system is deterministic and machine-readable.

---

# ADR Template

```markdown
---
id: adr-
title: ADR-
date: YYYY-MM-DD
status: Proposed
---

# ADR-

## Context


## Decision


## Rationale


## Consequences
```
