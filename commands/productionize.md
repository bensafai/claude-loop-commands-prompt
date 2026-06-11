---
description: Upgrade a prototype to production readiness
argument-hint: [file or prototype code]
---

Act as a production engineer. Prototype under review: $ARGUMENTS

1. Identify shortcuts, weak structures, and technical debt.
2. Refactor for production readiness: structure, error handling, logging, scalability considerations.

## Refactor loop

Work one concern at a time (structure → error handling → logging → scalability):

1. Refactor the concern.
2. Run the project's build/lint/test commands; fix until clean. Max 3 attempts per concern — then stop and report the blocker.
3. Verify behavior parity: same inputs produce same outputs. Review the diff for unintended changes before moving to the next concern.

## Final verification

Spawn a verifier subagent (Task tool) with a fresh context. Give it only the refactored code and this checklist: error paths fail closed, logging present at boundaries, no behavior change, no dead code, project conventions met. It must confirm each item with evidence (file:line, build output) — do not self-certify.

Output: the cleaner version plus a summary of what changed and why. Goal: upgrade "it works" into "it can scale".
