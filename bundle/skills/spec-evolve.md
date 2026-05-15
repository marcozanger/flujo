---
name: spec-evolve
description: Propose spec changes from observed reality (usage data, user feedback, technical findings). Different from /spec-revise — this one starts from evidence, not from a user instruction.
spec-fields: [FEATURE_TABLE, SUCCESS_METRICS]
---

# /spec-evolve

Use after `/usage-report`, support feedback waves, or a postmortem reveals that the spec is wrong.

## What to do
1. Take the input evidence (usage report, postmortem action items, support ticket cluster, whatever the user provides).
2. Spawn `spec-evolution-advisor` agent to propose specific section edits.
3. For each proposal, draft:
   - Section affected
   - Current text
   - Proposed text
   - Rationale grounded in the evidence (cite specifically — "usage report shows F7 at 4% adoption" not "F7 seems unused")
4. Present the proposal set to the user **before** writing.
5. Once approved, hand off to `/spec-revise` for each section. Each gets its own decision-log entry.

## Output
Markdown proposal in **{{WORKING_LANGUAGE}}** with one block per proposed change:

```
### §5 F7 Export — proposed change
**From:** Priority = MVP
**To:** Priority = Later
**Why:** 30d usage = 4%. Persona Marina (primary) never used it (`/usage-report` 2026-06-15).
**Risk if applied:** Removing from MVP means no export at v1.0 — acceptable per §10 success criteria.
```

Ask the user: *"Apply all / Apply some / Discard / Discuss."*

## Never
- Apply proposals without user approval, even if "obvious."
- Cite evidence vaguely. Always quote the specific report or ticket.
