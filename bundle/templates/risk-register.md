# Risk register — {{PROJECT_NAME}}

**Last audited:** {{TODAY}}
**Owner:** {{RACI_RESPONSIBLE}}

Risks are concrete dangers with a mitigation path. Unknowns to resolve go in `SPEC.md §12` TBDs, not here.

## Open risks (sorted by Probability × Impact)

| ID | Risk | Prob | Impact | Owner | Mitigation | Status | Updated |
|----|------|------|--------|-------|------------|--------|---------|
| R1 | {{SCARIEST_MVP_FEATURE}} — technical or adoption risk *(from Phase 3)* | M | H | {{RACI_RESPONSIBLE}} | Build it first (marked 🚨 in §5); validate via mockup before backend | open | {{TODAY}} |
| R2 | Budget cap of {{BUDGET}} vs MVP scope of {{MVP_FEATURE_COUNT}} features | M | H | {{RACI_ACCOUNTABLE}} | Re-prioritize at week 4 if burn exceeds plan | monitoring | {{TODAY}} |
| R3 | {{COMPLIANCE_REGIME}} compliance scope unclear *(if applicable)* | L | H | {{RACI_RESPONSIBLE}} | `/threat-model` before v1.0; consult legal | open | {{TODAY}} |

## Closed risks

| ID | Risk | Closed on | Outcome |
|----|------|-----------|---------|
| — | — | — | — |

## Audit cadence

Run `/risk audit` every 2 weeks during build, monthly post-launch. Every closure logs in `SPEC.md §13`.
