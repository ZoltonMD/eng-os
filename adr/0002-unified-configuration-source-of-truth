---
id: adr-0002
title: 'ADR-0002: Unified Configuration Source of Truth'
date: 2025-09-28
status: Proposed
---

# ADR-0002: Unified Configuration Source of Truth

## Context
Modern infrastructure suffers form "Split-Brain Configuration". Parameters are scattered across local files (`/etc`), 
environment variables, and distributed Key-Value stores (Consul/Etcd). When engineers make manual "hot-fixes" in any 
of these locations, the system enters an undocumented state known as **Configuration Drift**. This makes it 
impossible to reliably scale, audit, or recover from a disaster.

## Decision
We will enforce a unified "Source of Truth" hierarchy:
* **Level 1: Git is the Master.** No configuration change is "official" until it is committed to a Version Control 
system.
* **Level 2: The Automation Layer (The Producer).** Only CI/CD pipelines or Configuration Management 
(Ansible/Salt/Terraform) are permitted to write to production.
* **Level 3: The Runtime (The Consumer).** On-host files and Distributed KV stores are considered **Read-Only** 
targets.
    * **For Etcd/Consul:** Humans must not use the UI/CLI to edit values. A "Git-to-KV" sync tool must be used.
    * **For On-Host Files:** Local files must be managed by an agent that periodically "reconciles" (overwrites) 
    the state from the Git-backend master.


## Rationale
* **Unified Visibility:** An engineer shouldn't have to check three different UIs and ten servers to understand 
how a service is configured. They should only have to check **one Git repo**.
* **Disaster Recovery**: If a Consul cluster or a VM is destroyed, we can recreate the entire state from Git 
in minutes.
* **Peer Review**: Every change - whether it's a Nginx timeout or a feature flag in Etcd - must pass through a 
Pull Request.

## Consequences
* **Positive:**
    * **Elimination of "Snowflakes":** Every host and every KV-store entry is reproducible. We can wipe a cluster 
    and restore its exact state from Git in minutes.
    * **Auditability & Compliance:** We have a permanent record of every configuration change, including who 
    authorized it (via PR approval) and why.
    * **Drift Detection:** By using automated reconciliation, we can trigger alerts when a manual change is detected, 
    identifying unauthorized or "emergency" interventions immediately.
* **Negative:**
    * **Increased Latency for Changes:** A "simple" change now requires a Git commit, a Pull Request, and 
    a pipeline run. This can feel slow during high-pressure incidents.
    * **Pipeline Dependency:** If the CI/CD pipeline or the Git provider (e.g., GitLab/GitHub) is down, our ability 
    to reconfigure the system is blocked.
    * **Operational Complexity:** We must now manage the "Sync" tools (e.g., ArgoCD, Terraform, Cloud, or custom 
    Ansible AWX jobs) that keep Production in sync with Git.
* **Neutral:**
    * **Break-Glass Procedure:** We must define a formal "Emergency Access" protocol that allows manual edits during 
    a P1 incident, with a mandatory "Post-Incident Reconciliation" step to bring the changes back into Git.
