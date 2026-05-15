---
name: stress-test-spec
description: Adversarial pre-v1.0 read of SPEC.md + companion docs. Surfaces inconsistencies, implicit assumptions, edge cases not covered, and contradictions across sections. Run before marking v1.0 final.
spec-fields: []
---

# /stress-test-spec

Hand off to the `spec-stress-tester` agent (Opus 4.7). Goal: catch problems while they're still cheap to fix — in the spec, not in code.

## When to use
- Before declaring `Draft v0.x → v1.0 final`.
- After a large `/spec-revise` that touches multiple sections.
- Quarterly post-launch as a sanity check.

## What to do
1. Spawn `spec-stress-tester` agent. Pass it `SPEC.md` and the full `docs/` folder.
2. Show the user the findings grouped by severity (🔴 critical / 🟡 medium / 🟢 nit).
3. For each 🔴, propose a specific `/spec-revise` to resolve it.
4. Wait for user approval; do NOT auto-apply.
5. After the user resolves 🔴 findings, suggest re-running `/stress-test-spec` once for confirmation.

## Output

Markdown report in **{{WORKING_LANGUAGE}}** with severity-grouped findings, each citing the specific section(s) involved and an actionable suggestion. End with: *"Spec ready for v1.0 / Resolve [N] criticals first."*

## Constraints

- Never modify `SPEC.md` directly. This skill only proposes.
- Read-only across the entire `docs/` tree.
