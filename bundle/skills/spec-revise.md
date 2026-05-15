---
name: spec-revise
description: Revise a section of SPEC.md following the change protocol. Use when the user wants to update, add to, or rewrite a section of the spec. Bumps version, updates date, appends to decision log.
spec-fields: []
---

# /spec-revise

Apply the formal change protocol to `SPEC.md`. The spec is the source of truth — every change goes through this skill, never edit the file ad-hoc.

## When to use
- User says "revise the spec — section X — change Y"
- A feature scope, persona, or governance answer changed
- A `TBD` got resolved

## What to do
1. Read `SPEC.md` to confirm current `Status` and `Last updated`.
2. Apply the user's requested edit to the target section. Preserve everything else.
3. Bump version:
   - Draft → draft: `v0.x → v0.(x+1)`
   - First release: `Draft v0.x → v1.0`
   - Minor post-release: `v1.x → v1.(x+1)`
   - Breaking scope/stack/persona change post-release: `v1.x → v2.0`
4. Set `Last updated` to today (ISO `YYYY-MM-DD`).
5. Append a row to §13 decision log: `| date | new-version | one-line decision | rationale |`.
6. Tell the user which placeholders in the bundle changed (personas, features, stack, governance, look & feel, success metrics) and suggest running `/bundle-refresh` if any did.

## Communication
Reply in **{{WORKING_LANGUAGE}}**. Show the diff of what changed before saving, ask for confirmation.

## Never
- Edit `SPEC.md` without bumping version + appending to the decision log.
- Touch code in the same turn as a spec revision. Spec changes first, code follows.
