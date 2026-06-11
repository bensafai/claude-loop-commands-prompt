# claude-loop-commands

Claude Code slash commands with built-in self-correction loops: environment feedback, bounded retries, and fresh-context verifier subagents instead of self-critique.

## Why loops?

Most prompt collections tell the model *what to do*. These commands also define *how the model corrects itself*:

- **Environment feedback as ground truth.** Build output, exit codes, and test results decide whether a step is done — not the model's own judgment.
- **Bounded retries.** Every loop caps fix attempts (max 3), then reports the blocker instead of spiraling into blind retries.
- **Independent verification.** Models grade their own output poorly. Where it matters, a verifier subagent with a fresh context window confirms the result against a checklist with evidence (file:line, command output).
- **Measurable end states.** Conditions are written so they can be proven in the transcript ("build exits 0"), which makes them compatible with Claude Code's [`/goal`](https://code.claude.com/docs/en/goal) primitive for unattended runs.

## Install

Copy the command files into your project (or `~/.claude/commands/` for global availability):

```bash
mkdir -p .claude/commands
cp commands/*.md .claude/commands/
```

## Usage

Type `/` plus the command name in Claude Code (CLI or IDE plugin). Everything after the name becomes `$ARGUMENTS`:

```text
/elite-review src/auth/session.ts
/debug-system filter state resets after the grid re-renders
/implement-spec docs/feature-spec.md
/edge-cases                       ← no argument: reviews the current diff
```

Reference files with `@` to pull their content directly into the prompt:

```text
/elite-review @src/auth/session.ts
```

### Unattended runs with /goal

For long tasks, pair a command with `/goal` (Claude Code v2.1.139+). The goal evaluator checks the condition after every turn and keeps Claude working until it holds:

```text
/implement-spec docs/feature-spec.md
… approve the plan …
/goal every Definition of Done item is verified with evidence and the build exits 0, or stop after 30 turns
```

## Commands

| Command | Purpose | Loop |
| --- | --- | --- |
| `/architect` | System design before code: clarify → compare architectures → plan | Fresh-context reviewer subagent critiques the draft; one revision cycle |
| `/implement-spec` | Spec-driven implementation in vertical slices | Per-slice: build/lint feedback, max 3 fixes, DoD check; final verifier subagent |
| `/build-loop` | Incremental pair-building with approval gates | Build/lint before presenting; only working code reaches you |
| `/debug-system` | Root-cause analysis across components | Reproduce → fix → re-run reproduction → regression check; max 3 hypothesis cycles |
| `/perf` | Performance optimization | Baseline → one change → re-measure → keep/revert on evidence; experiment log |
| `/productionize` | Prototype → production readiness | One concern per iteration + parity check; verifier subagent certifies |
| `/edge-cases` | Failure-mode analysis | Evidence rule (file:line) + minimal reproductions; confirmed vs. theoretical |
| `/security-audit` | Security audit prioritized by risk | Traced attack paths; verifier subagent re-checks top findings |
| `/elite-review` | Strict code review with 1–10 rating | Evidence rule: every criticism cites actual code |
| `/multi-role` | Engineer + PM + DevOps merged into one plan | None — pure analysis, no environment feedback to correct against |

## Customization

The commands reference "the project's build/lint/test commands" and "the project's conventions" generically. They work best when your project defines these in a `CLAUDE.md` (build commands, style rules, security requirements) — Claude Code loads it automatically and the loops pick up the right commands. Without one, Claude will infer the commands from your package manifest, which usually works but is less deterministic.

## License

[MIT](LICENSE)
