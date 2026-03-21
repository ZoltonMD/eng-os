---
id: adr-0001
title: 'ADR-0001: Programmatic Maintenance State for Infrastructure'
date: 2025-09-13
status: Accepted
---

# ADR-0001: Programmatic Maintenance State for Infrastructure

## Context
* **The Noise**: On-duty engineers are frequently interrupted by "False Positive" alerts during 
planned maintenance, upgrades, or manual troubleshooting. 
* **The Fatigue**: Constant "Alert Fatigue" leads to real incidents being ignored. 
* **The Gap**: Manual silencing of alerts in a UI (like Grafana, Prometheus or OpsGenie) is often 
forgotten, leading to noise during the start of work, or (worse) alerts remaining silenced after 
the work is finished.

## Decision
We will implement a **Standardized Maintenance Lifecycle Library**. This library must be integrated 
into all automation (Ansible playbooks, CI/CD pipelines, and CLI tools).

### The Mechanism:
* **Source of Truth**: The maintenance state must be defined in a centralized **Inventory** or **CMDB** 
(e.g., Netbox tags, AWS Resource Tags, or a custom Metadata API)
* **Discovery**: Monitoring agents or centralized "Alert Managers" must poll this metadata to determine
if a target is in a "Mutable" state.
* **Local Override (Optional)**: A host-local flag can serve as a "Fast-Path" or fallback if the 
centralized API is unreachable, ensuring the system fails "quietly".
* **Self-Healing**: The state must include a **TTL (Time To Live)** to ensure a host automatically 
returns to "Monitored" status if an engineer forgets to disable maintenance mode.
  * **Default TTL**: A reasonable default (e.g., 2 hours) must be applied to all sessions.
  * **Overrides**: The library must provide the capability to override the default TTL for longer operations.
  * **Hard Limits**: To mitigate human error, a maximum TTL (e.g., 24-48 hours) must be enforced. Sessions exceeding this limit will require a manual extension or re-authorization.
* **API-First**: Monitoring systems must respect this local state and suppress notifications (but continue 
to collect data).

### Messaging & Audit Trail
* **Automated Notifications**: The library must emit an event to a centralized communication channel 
(e.g., `#aps-announcements` in Slack) at the `Start` and `End` of each maintenance window.
* **Mandatory Context**: Every maintenance activation requires a `reason` parameter.
  * *Example:*
    * Cmd:  
        ```
        maint --start --reason "Replacing faulty RAM stick - Ticket #402" host1-dc1
        ```
    * Slack message:   
        ```
        host1-dc1 put on maintenance for 2h
        Reason: "Replacing faulty RAM stick - Ticket #402"
        ```
* **Searchability**: This ensures that the Slack/Teams history serves as a human-readable "Audit Log", 
making it easy to correlate past system gaps with specific manual actions.

## Rationale
* **Reduced Cognitive Load:** By moving the "silencing" action into the same tool used for the work 
(the CLI or Playbook), we eliminate the need for the engineer to switch contexts to a Monitoring UI.
* **Human-Centric Design:** Forcing a "Reason" for maintenance creates an automatic, searchable audit 
trail in Slack. This replaces the "tribal knowledge" of who is doing what with a persistent system record.
* **Fail-Safe Reliability:** Implementing a **TTL (Time To Live)** prevents the "Permanent Silence" 
anti-pattern, where a host is accidentally left in maintenance mode for weeks after a task is finished.
* **Decoupling:** Using a centralized metadata store (CMDB/Tags) instead of a host-local file ensures 
that the maintenance state is visible to all auxiliary systems (Auto-scaling, Load Balancers, Security Scanners) 
simultaneously.

## Consequences
* **Positive**:
  * Significant reduction in "On-Call Noise". Improved trust in the alerting system.
  * High visibility for the whole team. No more "Who put this node in maintenance?" questions.
* **Negative**:
  * Small overhead in integration for new playbooks/services/tools.
  * Slight "friction" for the engineer who has to type a reason (but this friction is intentional to
  prevent mindless maintenance).
