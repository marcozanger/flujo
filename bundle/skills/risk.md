---
name: risk
description: Manage docs/risk-register.md — add, update, close, or list risks. Use whenever a new risk surfaces (technical, market, regulatory, dependency) or an existing one changes status.
spec-fields: [FEATURE_TABLE, NON_FUNCTIONAL, COMPLIANCE_REGIME]
---

# /risk

Subcommands: `add <description>` | `update <id>` | `close <id>` | `list` | `audit`.

## What to do

Spawn `risk-tracker` agent. It maintains `docs/risk-register.md` as a structured table with columns:

| ID | Risk | Probability (L/M/H) | Impact (L/M/H) | Owner | Mitigation | Status (open/monitoring/closed) | Updated |

Rules:
- New risks get auto-IDs (`R1`, `R2`, …) and `status=open`.
- Closing requires a rationale entry in the §13 decision log of SPEC.md.
- `audit` walks every open risk and re-asks: *"is this still real? still high-impact? mitigation still valid?"*
- High×High risks must have a mitigation. If none, flag as `BLOCKER: needs mitigation plan`.

## Output

In **{{WORKING_LANGUAGE}}**:
- For `add`: new row inserted + R-ID announced
- For `update/close`: diff vs previous state
- For `list`: top 5 risks sorted by probability × impact
- For `audit`: list of risks needing user attention

## Notes

- Risks ≠ TBDs. TBDs are unknowns to resolve; risks are known dangers to mitigate.
- Examples of risks: "vendor X may pull free tier", "F3 depends on undocumented internal API", "team lead leaves before v1.0", "GDPR ruling could force re-architecture".
