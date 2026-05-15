---
name: bundle-refresh
description: Re-emit skills/agents whose placeholder fields changed after a /spec-revise. Use whenever the spec change affected personas, features, stack, governance, look & feel, or success metrics.
spec-fields: [ALL]
---

# /bundle-refresh

Selective re-render of `.claude/skills/` and `.claude/agents/` based on which `spec-fields` each declares.

## What to do
1. Read the last entry of `SPEC.md` §13 to learn which sections changed.
2. Map sections → placeholders changed:
   - §1 → `VISION`
   - §3 → `PERSONAS_SUMMARY`
   - §4 → `JOURNEYS`
   - §5 → `FEATURE_TABLE`, `MVP_FEATURE_IDS`
   - §6 → `NON_FUNCTIONAL`, `COMPLIANCE_REGIME`
   - §7 → `TECH_STACK`, `INTEGRATIONS`
   - §8 → `LOOK_AND_FEEL`
   - §9 → `GOVERNANCE_BLOCK`
   - §10 → `SUCCESS_METRICS`
3. Scan every `.md` under `.claude/skills/` and `.claude/agents/`. For each file, read its `spec-fields:` frontmatter.
4. Re-render only the files whose `spec-fields` intersect the changed placeholders.
5. Show the user the list of files about to be regenerated, ask for confirmation, then write.

## Output
Summary in **{{WORKING_LANGUAGE}}**:
- Spec sections detected as changed
- Placeholders affected
- Files re-emitted
- Files left untouched (and why)

## Never
- Re-emit files whose `spec-fields` didn't change — that overwrites local edits unnecessarily.
- Run silently. Always show the regeneration list first.
