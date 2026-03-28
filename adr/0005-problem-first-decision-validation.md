---
id: adr-0005
title: 'ADR-0005: Problem-First Decision Validation'
date: 2026-03-28
status: Proposed
---

# ADR-0005: Problem-First Decision Validation

## Context
Engineering teams often Suffer from "Solutioneering" - the tendency to adopt new tools, languages, or architectural patterns because they are trending or "interesting", rather than because they address a specific pain point. Without a strict validation layer, the infrastructure becomes a collection of "solutions looking for a problem", leading to:
* **Feature Creep**: Excessive complexity that provides no business value.
* **Maintenance Toil**: Supporting tools that don't actually improve reliability or velocity.
* **Cognitive Overload**: Forcing the team to learn "hyped" check that isn't necessary for the current sale. 

## Decision
We will implement a mandatory "**Problem-First**" filter for every architectural change, tool adoption, or significant process shift.

Before any work begins, the proposer must provide a clear, one-sentence answer to the question:  
> **"What specific, measurable problem does this solve?"**

### The Rules of Engagement:
1. **No Problem = No Work**: If the proposer cannot define a current bottleneck, risk, or inefficiency, the proposal is automatically rejected.
2. **The "So What?" Test**: Once a problem is identified, we must ask: "What is the cost of not solving this?". If the cost is negligible, the task is deprioritized.
3. **Evidence-Based**: Problems should ideally be backed by metrics (e.g., "Our deployment takes 40 minutes", or "We have 5 manual interventions per week").

## Rationale
Every "unsolved" problem in an infrastructure creates **Toil**. Conversely, every "unnecessary" solution creates complexity.

In a high-velocity SRE environment, *Complexity is a Debt* that must be paid in maintenance hours, monitoring alerts, and cognitive load. By forcing a "Problem-First" validation, we ensure that we only take on new Debt when the "Revenue" (the problem solved) is higher than the "Interest" (the maintenance cost). This Prevents **Technical Vanity** and protects the team's capacity.

## Consequences
* **Pros:** Eliminates "Technical Vanity Projects".
    * Protects the team from arbitrary tasks.
    * Forces stakeholders to think in terms of **Value** rather than **Features**.
* **Cons:** May slow down the initial phase of "creative" brainstorming.
    * Might cause friction with stakeholders who are used to giving direct orders without justification.