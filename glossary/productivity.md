# Productivity Glossary

This document outlines the "Human Operating System" terminology. Understanding these concepts is essential to managing cognitive latency, protecting our focus-cycles, and maintaining high-availability mental performance.

| Term | Definition | Context / SRE Metaphor |
| :--- | :--- | :--- |
| **Attention Residue** | The "shadow" of a previous task that remains in the mind after switching, reducing the capacity for the new task. | **Memory Leak**. Fragments of the previous "process" still occupy mental registers, slowing down the execution of the current thread. |
| **Cognitive Closure** | The psychological desire for an answer or a finished state to end ambiguity. | An `Exit 0` code. The moment a task moves from "In Progress" to "Done", allowing the brain to release the resources associated with it. |
| **Context Encapsulation** | The practice of isolating all the information, tools, and logic required for a specific task within a single "Deep Work" window. | A *Docker Container* or a *Function Scope*. If a task is properly encapsulated, it doesn't "leak" into the next day's mental space. |
| **Context Switching** | The cognitive process of shifting attention between unrelated tasks, tools, or mental frameworks. | **Human Cache Miss.** The high cost of reloading "state" into mental RAM. Moving from an ADR to a Slack fire takes ~20 mins to "warm up" again | 
| **Deep Work** | Professional activities performed in a state of distraction-free concentration that push cognitive capabilities to their limit. | **Batch Processing.** Running a long-running, high-priority job with exclusive locks on system resources to ensure maximum throughput and quality. |
| **Definition of Done (DoD)** | A strict, pre-defined checklist that must be met for a task to be considered complete. | *CI/CD Health Checks*. If the DoD isn't met, the "Segment" cannot roll, and the loop stays open. |
