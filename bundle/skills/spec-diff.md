---
name: spec-diff
description: Compare two versions of SPEC.md and summarize what changed. Use when reviewing a spec revision, prepping a stakeholder update, or auditing scope creep.
spec-fields: []
---

# /spec-diff

Semantic diff of `SPEC.md` between two git refs, grouped by section.

## Arguments
- `<ref>` — git ref to diff against (default `HEAD~1`).
- `<ref-a>..<ref-b>` — explicit range.

## What to do
1. Run `git show <ref>:SPEC.md` and compare against current `SPEC.md` (or both refs if range given).
2. Group changes by spec section (1–14).
3. For each changed section, summarize in 1–3 bullets what changed conceptually, not line-by-line.
4. Flag scope-impacting changes explicitly:
   - Features moved between MVP / v1.x / Later / Cut
   - Personas added/removed
   - Tech stack swaps
   - Compliance regime changes
5. Pull every new row from §13 decision log into the report.

## Output

Markdown summary in **{{WORKING_LANGUAGE}}**:

```
# Spec diff <ref-a> → <ref-b>

## §3 Personas
- Added persona "Marina (freelance)" with goal X

## §5 Features  ⚠️ scope-impact
- F7 moved MVP → Later
- F12 added at Later priority

## Decisions logged
- YYYY-MM-DD v0.4 — <one-liner>
```

End with: *"Affected bundle placeholders: <list>. Run `/bundle-refresh` to re-emit."* — only if scope-impacting fields changed.

## Never
- Run destructive git commands. Read-only diff.
