---
name: review
description: Review the current branch (or a PR) against the SPEC.md, not a generic checklist. Use before merging. Catches spec drift, missing tests for stated journeys, and scope creep.
spec-fields: [FEATURE_TABLE, JOURNEYS, NON_FUNCTIONAL, COMPLIANCE_REGIME]
---

# /review

Arguments: optional `<PR-number>` or `<branch-name>`. Defaults to current branch vs main.

## What to do
1. Diff branch against `main` (or fetch the PR).
2. Identify which §5 feature(s) this PR claims to implement (commit messages, branch name, PR title).
3. For each claimed feature:
   - Verify acceptance criterion from §5 Notes is met by the code.
   - Verify a journey-aligned test exists (per `/test` convention).
   - Verify no unrelated features got modified silently — that's scope creep.
4. Run the type-specific check via the right agent:
   - Web → spawn `a11y-web-auditor` if any UI changed.
   - Flutter → spawn `a11y-flutter-auditor` if any screen changed.
   - Spreadsheet → spawn `formula-auditor` if formulas/scripts changed.
5. Run `security-reviewer` agent if the diff touches auth, data persistence, or anything covered by §6 compliance.

## Output
Markdown review in **{{WORKING_LANGUAGE}}** with:
- ✅ what's good
- ⚠️ what to fix before merge
- ❌ blockers
- One sentence: *"Merge / Don't merge / Merge after fixing <list>."*

## Never
- Approve a PR that touches a feature whose spec acceptance criterion is `TBD`.
- Approve a PR that adds a feature not in §5.
