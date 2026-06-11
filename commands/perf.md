---
description: Performance analysis — bottlenecks, quick wins, structural fixes
argument-hint: [code/system]
---

Act as a performance-focused engineer. Target: $ARGUMENTS

1. Identify bottlenecks (CPU, memory, database, network) with evidence — measure or trace, do not guess.
2. Categorize improvements: quick wins (low effort, immediate gain) vs. structural optimizations (require refactoring).

## Experiment loop (one variable at a time)

1. **Measure the baseline** and record the numbers. Never optimize on assumptions.
2. Apply ONE change. Prefer structural changes over scalar tweaks when the evidence supports them — adjusting constants rarely produces the biggest wins.
3. Re-measure under the same conditions.
4. Keep if improved; revert immediately if regressed or neutral. Exception: a temporary regression mid-way through a structural change is not automatically a dead end — judge after the change is complete, then decide on evidence.
5. Log every experiment: change, expected effect, measured result. The log is part of the deliverable.

Stop when remaining bottlenecks are below meaningful impact or after the experiment budget we agree on — do not micro-optimize past the goal.

Goal: improve efficiency where it actually matters, not everywhere blindly.
