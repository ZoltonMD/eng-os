---
id: adr-0004
title: 'ADR-0004: Disaster Recovery Strategy and RPO/RTO Targets'
date: 2026-03-24
status: Proposed
---

# ADR-0004: Disaster Recovery Strategy and RPO/RTO Targets

## Context
Currently, we lack formalized recovery objectives for critical failures (e.g., region-wide outages or massive data corruption).
* **The Problem:** Without defined metrics, engineers either over-engineer for high availability (increasing costs) or build systems that are impossible to recover within business-acceptable timeframes.
* **The Risk:** In a catastrophic event, the business could face 24+ hours of data loss or a week of downtime, leading to irreparable financial and reputational damage.

## Decision
We will classify all services into **Recovery Tiers** with mandatory compliance targets:

| Tier | Description | RPO (Max Data Loss) | RTO (Max Downtime) | Strategy |
| :--- | :--- | :--- | :--- | :--- |
| Tier 0 | Identity & Financial Gateway (Payments, Auth) | < 1 min | < 15 min | Multi-region Active-Active |
| Tier 1 | Core Service Logic | < 15 min | < 2 hours | Warm Standby (Pilot Light) |
| Tier 2 | Analytical & Backoffice Tools | < 4 hours | < 24 hours | Cold Backup / Rebuild from IaC |

* **Immutable Backups:** All backups must be stored in an "Off-site" locations (cross-account/cross-region) with **Object Lock** enabled to prevent Ransomware or accidental deletion.
* **Infrastructure as Code (IaC)**: Full environment recovery must be automated. Manual intervention for core infrastructure setup is prohibited during a DR event.
* **Regular Drills:** We will conduct semi-annual "Game Days" to simulate failures and verify our actual RTO/PRO against these targets.
  * **The Standard:** DR procedures must be documented in a **Runbook** and tested during "Game Days".
* **Degraded Mode (Optional):** Instead of a full recovery, we only bring up the "Read-Only" version of the app first (where it's applicable). It's cheaper and faster, and it keeps users from seeing a 504 error while we work on the "Write" capability.

## Rationale
* **Cost Efficiency:** We avoid expensive Active-Active setups for non-essential services (Tier 2).
* **Alignment:** The CTO and stakeholders now have a clear "Insurance Policy" and understand the financial risks of each Tier.
* **Reliability:** Automated Recovery reduces "Human Error" during high-stress incidents.

## Consequences
* **Positive:** Predictable business continuity. Clear technical requirements for new features.
* **Negative:** Increased operational overhead for maintaining and testing the DR site. Storage costs for immutable backups.
