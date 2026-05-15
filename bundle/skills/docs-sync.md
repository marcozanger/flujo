---
name: docs-sync
description: Keep README, CHANGELOG, and other docs in sync with SPEC.md. Use after a /spec-revise or before a release.
spec-fields: [VISION, MVP_FEATURE_IDS, FEATURE_TABLE, SUCCESS_METRICS]
---

# /docs-sync

Mechanical sync of derived docs from `SPEC.md`. Spec is canonical — these docs are projections of it.

## What to do
1. Spawn `doc-keeper` agent.
2. Update or create:
   - `README.md` — pull §1 vision phrase as the tagline, §1 elevator pitch as the intro, current MVP features as the feature list.
   - `CHANGELOG.md` — append entries derived from §13 decision log since last release.
   - `CONTRIBUTING.md` — if it exists, ensure the change-protocol section points at `SPEC.md` §13.
3. If `{{PROJECT_TYPE}}` = Spreadsheet: regenerate the "Handoff" sheet/doc from §9 maintenance answers.

## Output
List of files updated in **{{WORKING_LANGUAGE}}**, with a one-line summary per file. No diff dump.

## Never
- Invent feature copy. Pull verbatim from `SPEC.md`.
- Edit anything outside the derived-doc set.
