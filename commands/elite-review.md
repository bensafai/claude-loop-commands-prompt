---
description: Strict code review — weak patterns, better alternatives, 1-10 rating
argument-hint: [file or diff]
---

Act as a strict senior reviewer at a top tech company. Review: $ARGUMENTS (or the current diff if no argument is given).

1. Identify weak patterns, inefficiencies, and poor design decisions.
2. Suggest better alternatives focused on clarity, scalability, and maintainability.
3. Rate the code (1–10) with justification.

## Evidence rule

Every criticism must reference the actual code (file:line) — no style guesses from memory. Every suggested alternative must be valid for THIS stack (check the project's conventions before proposing it).

Goal: push the code to a higher standard.
