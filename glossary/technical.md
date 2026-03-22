# Technical Glossary

This document defines the core terminology used across out architecture to ensure clear communication and prevent "Cognitive Load".

| Term | Definition | Context/Example |
| :--- | :--- | :--- |
| **Availability** | | |
| **Circuit Breaker** | A design pattern used to detect failures and encapsulate the logic of preventing a failure from constantly recurring. | Implemented in Gateway for all 3rd parti auth providers. |
| **Configuration Drift** | The phenomenon where the actual state of a running system diverges from the "Source of Truth" (Git/IaC) due to manual ad-hoc changes or silent failures in automation. | *Example:* An SRE increases a timeout on a specific server via CLI to fix a latency spike. This change isn't in Git, so the next automated deployment "drifts" the server back to the old, broken state. |
| **Disaster Recovery (DR)** | A set of policies, tools, and procedures to enable the recovery or continuation of vital technology infrastructure and systems following a natural or human-induced disaster. | DR depends on **Immutability**. If your configuration is "drifted", you cannot reliably recreate your environment in a new region during a total data center failure. |
| **Idempotency** | The property of certain operations that can be applied multiple times without changing the result beyond the initial application. | Crucial for API retry logic. |
| **Monitoring** | A subset of observability. It's the practice of tracking a system's health by collecting predefined metrics to trigger alerts when thresholds are breached. It focuses on *symptoms* (the "what") rather than *exploration* (the "why"). | To provide real-time visibility into the "known" state of a system and ensure it operates within expected parameters (SLOs). |
| **Observability** | The ability to explain any system state, no matter how novel or bizarre, without having to ship new code. | Decrease the **MTTI** (Mean Time to Identification) of root causes by ensuring high-cardinality data is available in our telemetry. |
| **SLO** | **Service Level Objective**. A specific target value for a service level that is measured by an SLI (Service Level Indicator). It represents the "Goal" for your system's reliability. | To create a data-driven "line in the sand" that balances the need for feature velocity with the need for system stability. |
