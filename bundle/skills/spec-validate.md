---
name: spec-validate
description: Lint SPEC.md against the canonical template. Use to find missing sections, unresolved TBDs without owners, MVP features missing justification, or stale "Last updated" dates.
spec-fields: []
---

# /spec-validate

Static check of `SPEC.md` against the template the spec generator emitted.

## What to do
1. Read `SPEC.md`.
2. Check each numbered section exists (1–14) and is non-empty.
3. For §5 Functional requirements: every row with `Priority = MVP` must have a non-empty `Notes` column. Flag rows that don't.
4. For §12: every `TBD` in the doc must appear in §12 with a `needs <X>` note. Flag orphan TBDs.
5. Check `Last updated` ≤ 30 days old; if older, flag as `stale-header`.
6. Check §13 has at least one entry per minor-version bump.

## Output
A markdown report in **{{WORKING_LANGUAGE}}** with three buckets:
- `❌ Blocking` — empty section, MVP-without-justification, orphan TBD.
- `⚠️ Warning` — stale header, missing decision-log entry.
- `✅ OK` — sections that passed.

End with a single suggested next action (e.g. *"Run `/spec-revise` on §3 to resolve TBDs about persona constraints"*).

## Never
- Modify `SPEC.md`. This skill is read-only.
