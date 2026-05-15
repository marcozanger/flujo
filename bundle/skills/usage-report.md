---
name: usage-report
description: Pull product metrics and compare them to SPEC.md §10 success criteria. Use at 30-day and 90-day post-launch checkpoints.
spec-fields: [SUCCESS_METRICS, PERSONAS_SUMMARY, MVP_FEATURE_IDS]
---

# /usage-report

Arguments: `30d` | `90d` | `<custom-window>`.

## What to do
1. Read `SPEC.md` §10. Identify the metrics defined for the requested window.
2. Ask the user where the metrics come from (analytics tool, DB query, internal dashboard). If unknown, record as TBD and produce a partial report.
3. Pull or request the metric values for the window.
4. For each metric, compute: **target** (from §10) vs **actual** vs **delta** (% and absolute).
5. Spawn `usage-analyzer` agent to propose 2–3 hypotheses for each significant miss.
6. Identify which MVP features are under-used vs heavily-used.

## Output
Markdown report in **{{WORKING_LANGUAGE}}**:

```
# {{PROJECT_NAME}} — 30d report (YYYY-MM-DD)

## Success criteria
| Metric | Target | Actual | Δ |
|---|---|---|---|
| Activation rate | 40% | 28% | -12pp ⚠️ |

## Feature usage
- F1 Login: 100% sessions
- F7 Export: 4% sessions ⚠️ low

## Hypotheses (from usage-analyzer)
1. …
```

End with: *"Suggested follow-ups: `/spec-evolve` on §5 to deprioritize F7? Spawn `persona-prober` on F1 → F7 journey?"*
