---
name: bug
description: Triage and fix a bug, anchoring on the spec. Classifies which persona/feature/journey is affected before fixing, so the fix is scoped to spec reality, not symptoms.
spec-fields: [PERSONAS_SUMMARY, FEATURE_TABLE, JOURNEYS]
---

# /bug

Arguments: `<issue-url>` or `<short description>`.

## What to do
1. Reproduce the bug (or ask the user for repro steps if not provided).
2. Identify the affected persona(s) from §3 and feature ID(s) from §5.
3. Identify the journey from §4 that's broken.
4. Decide bug class:
   - **Spec-faithful bug** — code doesn't match what spec says. Fix the code.
   - **Spec gap** — spec is ambiguous. Stop, run `/spec-revise` first, then fix.
   - **Spec-incorrect bug** — spec says something that turned out to be wrong in practice. Stop, run `/spec-evolve`, then fix.
5. Fix only the smallest change that resolves the issue. No drive-by cleanup.
6. Add a regression test named after the persona + scenario.

## Output
A short report in **{{WORKING_LANGUAGE}}**:
- Persona/feature/journey hit
- Bug class
- Root cause (one paragraph)
- Files changed
- Regression test added

If you spawned `bug-hunter`, summarize its findings here.
