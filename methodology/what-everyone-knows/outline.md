# Book Roadmap: What Everyone Knows

## The Vision
To bridge the gap between "Hard" SRE skills and the "Soft" cognitive mechanics required to survive high-scale 
infrastructure.

> **Status:** 🏗️ Active Development  
> This outline is a living document. It will be updated, re-ordered, and expanded as the project matures and new insights are codified.

## The Layers

### Layer 0: Beyond the System
* **0.01 Introduction:** The "Cache Warming" of the mind.
* **0.02 Warning:** Why you should be careful reading this.
* **0.03 From Author:** How to read this book.

### Layer 1: Human Runtime (Focus)
* **1.01 The One-Hour Constraint:** Why exclusive resource locking is needed for deep work.
* **1.02 Splitting Tasks to Chunks:** Why it's important to split big monolith tasks, and how it helps us on several 
levels.
* **1.03 "Two Minutes" Rule (GTD):** Handling "Interrupts" immediately if the overhead of scheduling them is higher 
than the execution time.
* **1.04 Give your thoughts to paper:** "Externalizing Memory" to clear the registers and reduce cognitive load.

### Layer 2: The Scheduler (Priority)
* **2.01 Plan, Organize, Do:** Defining the "Job Scheduler" logic for the day.
* **2.02 80/20 Principle:** Identifying the "Critical Path" tasks that provide the most system value.
* **2.03 Counting Task Estimation:** "Resource Allocation" forecasting.
* **2.04 Distributing tasks by days:** "Load Balancing" the weekly workload to avoid spikes.
* **2.05 Limit the number of ongoing tasks (WIP Limits):** Preventing "Thrashing" by limiting the number 
of active threads.
* **2.06 Get rid of "idle" non-vital tasks:** "Cleaning the Queue". If a task doesn't add value, `SIGKILL` it.

### Layer 3: Automation (Toil Reduction)
* **3.01 Doing something a second time - Automate it:** The core SRE principle of eliminating repetitive 
manual work.
* **3.02 Async conversation:** Moving from "Synchronous Blocking" (Instant messaging) to "Asynchronous Queueing" 
(Email/Jira)
* **3.03 Not every message is urgent:** Implementing "Backpressure" and "Rate Limiting" on your availability. (This 
is where **Poka-Yoke** fits - designing a system where it's hard to make a mistake, like having "Do Not Disturb" as 
a default)

### Layer 4: Maintenance & Health (Reliability)
* **4.01 Don't break the chain (15min reflection):** The "Daily Health Check" and log rotation at the end of 
the shift.
* **4.02 Celebrate even small accomplishments:** "Positive Feedback Loops" to maintain system morale.
* **4.03 Switching off from work:** "System Shutdown/Sleep Mode". The brain must recharge to clear the 
"Attention Residue" (Memory Leaks).
