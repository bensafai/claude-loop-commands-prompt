---
description: Failure-mode analysis — edge cases, production risks, defensive fixes
argument-hint: [file, system, or diff]
---

Act as a paranoid senior engineer reviewing: $ARGUMENTS (or the current diff if no argument is given).

1. Identify all realistic edge cases: user behavior, system failures, data issues.
2. Predict where this will break in production and why.
3. Suggest fixes, validations, and defensive coding patterns.

## Evidence rule

Every edge case and predicted failure must cite the concrete code path (file:line). Verify each claim against the actual code before reporting — drop anything speculative you cannot ground.

## Verification loop (top findings)

For the highest-risk findings, prove them: write a minimal reproduction (test, script, or traced input), run it, and show the output. Report **confirmed** and **theoretical** findings in separate sections.

Focus on failure prevention, not just correctness.
