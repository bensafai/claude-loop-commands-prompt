---
description: Spec-driven implementation — align first, then build in vertical slices
argument-hint: [path to spec document]
---

Implement the feature specified in: $ARGUMENTS

The spec is the single source of truth and the ONLY feature in scope. Read it in full before anything else.

**Role:** staff-level architect working as my pair. Bias toward working, shippable vertical slices over exhaustive upfront design. The simplest architecture that satisfies the spec wins — no abstractions "for later", no over-engineering.

**Project constraints:** the project's convention files (CLAUDE.md, contributing guide, lint configs) apply in full and win on conflict with the spec — flag any conflict instead of silently resolving it.

## Phase 1 — Align (STOP at the end; write NO feature code until I approve)

1. Read the spec end to end.
2. Clarify only what is genuinely ambiguous or risky: data contracts (inputs/outputs, shapes, error codes); state and lifecycle; error/loading/empty/edge states; component boundaries and interfaces; permissions and trust crossings; non-functional constraints. Challenge assumptions; name gaps and contradictions. No generic questionnaire.
3. Plan (one page max): components with single responsibilities, data flow between them, key interfaces. Name the riskiest assumption.
4. Wait for my go.

## Phase 2 — Build (after approval)

Work in vertical slices, not file-by-file. A slice = one coherent capability that builds and is independently reviewable.

Per-slice self-correction loop:

1. State in 1–2 lines what the slice covers and why it's next. Implement it fully across every layer it touches.
2. **Collect environment feedback:** run the project's build/lint/test commands and surface the output — exit codes and errors are the ground truth, not your own judgment.
3. On errors or new warnings: fix and re-run. Max 3 attempts — then stop and report the blocker instead of guessing.
4. Check the slice against the Definition of Done below, citing evidence (file:line, command output).
5. Stop at the slice boundary for my review — not after every function.

## Final verification (after the last slice)

Spawn a verifier subagent (Task tool) with a fresh context. Give it ONLY the spec path and the Definition of Done; it must independently confirm each item with evidence. Independent grading beats self-critique — do not self-certify. Fix what it rejects, re-verify once.

## Definition of Done (per slice and overall)

- [ ] Matches the spec; any deviation flagged and justified.
- [ ] Builds clean — no errors, no new warnings; core path verified, no runtime/console errors.
- [ ] Conforms to the project's conventions (style, naming, framework idioms, security rules).
- [ ] Error / edge / empty / loading states handled. Fail closed, not open.
- [ ] No dead code, no silent TODOs, no unrelated files touched.

**Scope guardrails:** touch only files this feature needs. Ask before creating new top-level directories, adding dependencies, or changing build/config.

**Unattended runs:** pair with /goal after approval, e.g.
`/goal every Definition of Done item is verified with evidence and the build exits 0, no unrelated files modified, or stop after 30 turns`
