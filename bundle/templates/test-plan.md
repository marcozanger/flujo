# Test plan — {{PROJECT_NAME}}

**Derived from:** `SPEC.md` §5 features × §4 journeys × §6 non-functional targets.
**Coverage goal:** every MVP row in §5 has at least one Unit + one Integration + one Journey test.

## Coverage matrix

| Feature | Unit | Integration | E2E / Journey | Manual / Exploratory | Notes |
|---------|------|-------------|---------------|----------------------|-------|
| F1 (MVP) | ✅ | ✅ | ✅ J1 | ✅ Marina handheld | Acceptance: <2s response |
| F2 (MVP) | ✅ | ⚠️ TBD | ❌ | — | Integration test pending DB schema |

*(Fill from {{FEATURE_TABLE}} — every MVP row must appear.)*

## Test layers

- **Unit** — pure logic, <50ms each, no I/O.
- **Integration** — boundaries with real DB / API / file system; mock external services only.
- **E2E / Journey** — one per §4 journey; named after persona + outcome (`test_marina_sees_runway_within_2s`).
- **Manual / Exploratory** — persona-led walkthroughs; record findings in `docs/exploratory-notes/`.

## Non-functional coverage

| §6 target | How verified | Owner |
|-----------|--------------|-------|
| First paint <2s on 4G | Lighthouse CI on PR | Frontend |
| 99.9% availability | Uptime monitor in prod | SRE |
| WCAG 2.1 AA | `a11y-{{PROJECT_TYPE}}-auditor` agent on every PR | Frontend |
| {{COMPLIANCE_REGIME}} controls | Audit log review + `security-reviewer` agent | Security |

## Cadence

- On PR: unit + integration must pass; e2e for affected journeys.
- Pre-release: full e2e + manual exploratory pass + `regression-watcher` agent.
- Post-incident: add regression test before closing the bug.

## Open gaps

- [ ] No load testing setup yet
- [ ] No accessibility audit automation
