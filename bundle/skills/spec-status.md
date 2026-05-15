---
name: spec-status
description: Executive summary of SPEC.md. Use when the user wants a quick read of what's confirmed, what's TBD, and how complete the spec is by phase.
spec-fields: []
---

# /spec-status

One-page overview of `SPEC.md`. Snapshot view, not a lint.

## What to do
1. Read `SPEC.md`.
2. Compute per-phase completeness (Phase 1 vision → Phase 9 rollout):
   - `complete` — section exists, no TBDs.
   - `partial` — section exists, has TBDs.
   - `missing` — section empty or absent.
3. Count features by priority bucket from §5.
4. List open TBDs from §12 grouped by phase.
5. Show last 3 entries from §13 decision log.

## Output

Markdown report in **{{WORKING_LANGUAGE}}**:

```
# {{PROJECT_NAME}} — spec status (v<x.y>, updated YYYY-MM-DD)

## Completeness
- Phase 1 Vision: ✅
- Phase 2 Personas: ⚠️ 1 TBD
- Phase 3 Features: ✅ (MVP=N, v1.x=M, Later=K)
- … etc.

## Open TBDs (count)
- §3 Personas (1)
- §6 Non-functional (2)

## Recent decisions
- YYYY-MM-DD v0.4 — <decision>
```

End with a single recommended next move.

## Never
- Modify any file. Read-only.
