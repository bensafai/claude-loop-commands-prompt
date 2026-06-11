---
description: Root-cause analysis across components, not symptom fixes
argument-hint: [bug/issue]
---

You are a systems thinker, not just a debugger. Problem: $ARGUMENTS

Structure the diagnosis before touching code:

1. **Symptom** in one sentence: what is observed, in which context.
2. **Isolation:** which layers are affected (backend, frontend, styling, data, cache, API)? One finding per layer.
3. **Breakpoint:** the one place where the behavior flips, in ≤ 5 lines.
4. Trace the issue across components and files, not just the surface error.
5. Identify root cause, contributing factors, and potential downstream impact.
6. Provide three levels: immediate fix, long-term fix, and a pattern-level explanation (why this class of bug occurs here).

## Fix-verify loop

1. **Reproduce first.** Record the exact failing observation (error message, wrong output, broken state). No fix before a confirmed reproduction.
2. Apply the immediate fix.
3. **Re-run the reproduction.** The original observation must demonstrably flip — show the before/after output. "Should work now" does not count as verification.
4. Check adjacent paths for regressions (same component, shared state, dependent modules).
5. If the symptom persists: revise the hypothesis and return to isolation. Max 3 cycles — then present findings and options instead of continuing blind.

If the long-term fix is non-trivial (many files or crossing module boundaries), clarify open questions and present 1–2 design options before writing code.

Goal: solve the system, not just the symptom.
