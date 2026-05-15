---
name: implement
description: Implement a specific feature from SPEC.md by ID. Use when starting work on F1, F2, etc. Loads the feature spec, its persona owner, and acceptance criteria into context before coding.
spec-fields: [FEATURE_TABLE, PERSONAS_SUMMARY, TECH_STACK]
---

# /implement

Arguments: `<FeatureID>` (e.g. `F3`).

## What to do
1. **Mockup gate.** Check that `mockup/` exists and the user has signed off on the journey this feature participates in. If no mockup or no signoff, stop and tell the user: *"Run `/mockup` first and validate the navigation + look & feel with stakeholders before we write real code. This catches scope/UX issues 10× cheaper than fixing them post-implementation."* Only proceed if the user explicitly overrides ("skip mockup, build directly").
2. Read `SPEC.md` §5 and pull the row for `<FeatureID>`. If priority ≠ MVP, ask the user to confirm scope-creep before proceeding.
3. Pull the persona(s) from §3 that own this feature.
4. Pull the journey from §4 this feature participates in.
5. Restate the feature in three lines: *what*, *for whom*, *acceptance criterion*. Ask the user to confirm before writing code.
6. Plan the change: list files to touch, propose names for new files, surface architectural questions. **Cross-reference the mockup** — the implemented screen should match the mocked screen for that journey step unless the spec explicitly diverges.
7. Implement, following the stack defined in §7 (`{{TECH_STACK}}`).
8. Stop before opening a PR. Hand off to `/test <FeatureID>` for tests, then `/review` for review.

## Constraints
- Communicate in **{{WORKING_LANGUAGE}}**.
- Never invent feature scope. If the spec is ambiguous, ask — don't decide.
- If reality forces a divergence from the spec, stop, propose a `/spec-revise`, and resume only after the spec is updated.

## Output
A short summary: feature restated, files touched, tests still to write, open questions.
