---
name: dep-update
description: Update project dependencies safely. Runs tests after each batch, splits major bumps from patch/minor, flags any dep that affects §7 stack or §9 compliance.
spec-fields: [TECH_STACK, COMPLIANCE_REGIME]
---

# /dep-update

Arguments: optional `--major` to include major-version bumps.

## What to do
1. Spawn `dep-updater` agent to enumerate available updates.
2. Group them:
   - **Patch & minor** — bump in one batch.
   - **Major** — one bump per branch, separate review.
   - **Stack-critical** — anything in §7 chosen stack. Stop and ask user before bumping.
   - **Compliance-relevant** — anything that handles auth, crypto, data export, or appears in a §9 governance answer. Spawn `security-reviewer` after bumping.
3. After each batch:
   - Run the test suite.
   - Run `/review` against the diff.
4. Open one PR per group.

## Output
Summary in **{{WORKING_LANGUAGE}}**:
- Batches applied
- Tests results per batch
- Open follow-ups (major bumps not yet applied)
- Any new security review needed

## Never
- Bump a major version of a §7 framework without explicit user approval.
- Skip tests after a batch.
