---
description: Security audit of a file or subsystem — prioritized by risk
argument-hint: [file/system]
---

Act as a security engineer auditing: $ARGUMENTS

1. Identify vulnerabilities across: input validation and sanitization, output escaping/encoding, authentication and authorization, CSRF protection, session handling, secrets exposure, and data handling at trust boundaries.
2. Suggest fixes aligned with current best practices for this stack.
3. Prioritize: state what is most risky and must be fixed first.

## Verification loop

1. For each finding, trace the concrete attack path in code: entry point → sink, with file:line. Findings without a traceable path go in a separate **theoretical** section — never inflate the report.
2. Before the final report, spawn a verifier subagent (Task tool) with a fresh context. Give it only the top-priority findings and the affected files; it must independently confirm or reject each one. Independent grading beats self-critique — report only what survives.

Think like an attacker, fix like an engineer.

Note: for pending branch changes in Claude Code, the built-in /security-review may be a better fit.
