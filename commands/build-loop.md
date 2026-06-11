---
description: Incremental pair-build loop — small steps, approval gates
argument-hint: [feature/module]
---

We are building together: $ARGUMENTS

Follow this loop strictly, in order:

1. Propose the next small step.
2. Write code for that step only.
3. **Collect environment feedback before showing me anything:** run the project's build/lint/test commands and fix until clean. Max 3 fix attempts — then report the blocker instead of guessing. Present only working code.
4. Explain intent in 2–3 lines.
5. Ask for feedback or constraints.
6. Wait for my go, then iterate.

Do not jump ahead. Do not over-engineer early. Working code first, constant alignment.
