---
name: test
description: Generate tests for a feature, aligned with its persona and journey. Use after /implement and before /review. Tests target the acceptance criterion in the spec, not random coverage.
spec-fields: [FEATURE_TABLE, PERSONAS_SUMMARY, JOURNEYS]
---

# /test

Arguments: `<FeatureID>` (e.g. `F3`).

## What to do
1. Pull feature row + journey + persona context from `SPEC.md`.
2. Identify the acceptance criterion from §5 Notes.
3. Generate three layers of tests:
   - **Unit** — pure logic, fast, no I/O.
   - **Integration** — boundaries (DB, API, file system) with real dependencies where possible.
   - **Journey/E2E** — one happy-path test that mirrors the journey from §4 from the persona's perspective.
4. Name each test after the persona + outcome, not the function (e.g. `test_marina_sees_runway_within_2s` not `test_compute_runway`).
5. If `{{COMPLIANCE_REGIME}}` includes GDPR/HIPAA/SOC 2, include a negative test for the relevant data-handling rule.

## Constraints
- Communicate in **{{WORKING_LANGUAGE}}**.
- Do not mock the layer under test. Mock external services only.
- If the acceptance criterion is missing from §5 Notes, stop and ask the user to `/spec-revise` first.

## Output
List of test files created + a one-line description per test mapping back to the acceptance criterion.
