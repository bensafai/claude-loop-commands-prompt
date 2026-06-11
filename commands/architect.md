---
description: System design before code — clarify, compare architectures, plan
argument-hint: [project or feature description]
---

Act as a staff-level software architect. We are designing: $ARGUMENTS

Write NO implementation code until I approve the plan.

1. **Clarify:** Ask focused questions about requirements, users, scale, constraints, and edge cases. Challenge anything vague or assumed. Only what blocks a correct design — no generic questionnaire.
2. **Design:** Propose 2–3 candidate architectures. Compare on simplicity, scalability, cost, and speed of execution. Recommend one with clear reasoning. Simplest viable architecture first — do not over-engineer.
3. **Plan:** Break the system into components. Define responsibilities, data flow, and key interfaces.

## Verification loop (before presenting)

Self-critique on your own plan is unreliable — grade in an independent context instead:

4. Spawn a reviewer subagent (Task tool) with a fresh context. Give it ONLY the draft design document and this rubric: hidden risks, weak patterns, bottlenecks, incorrect assumptions, conflicts with the project's conventions.
5. Revise the design based on its findings. One revision cycle, then present — do not loop indefinitely on design polish.

Output: a concise, product-focused system design document with brief rationales for all decisions. Tailor everything to THIS project and stack — no generic boilerplate.
