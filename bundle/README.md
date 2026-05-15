# Bundle — Skills & Agents

Plantillas que el spec generator emite junto al `SPEC.md` al final de la Fase 9. Cada archivo se renderiza interpolando datos del spec, así los agentes son específicos al proyecto en cuestión, no plantillas genéricas.

## Estructura entregada al usuario

El output se escribe en **`projects/<slug>/`** dentro de este repo `flujo`. Esa carpeta está **gitignoreada** para mantener la meta-info (instructions, templates, agents) separada de los proyectos generados. El usuario después mueve / `git init` ese subdirectorio para hacerlo su proyecto propio.

```
flujo/                                ← este repo (meta-project, en git)
├── project-instructions.md
├── bundle/                           ← templates en git
│   ├── skills/
│   ├── agents/
│   └── templates/
├── .gitignore                        ← incluye `projects/`
└── projects/                         ← outputs (NO en git)
    └── <slug>/
        ├── SPEC.md
        ├── docs/
        │   ├── risk-register.md
        │   ├── data-model.md
        │   ├── architecture.md
        │   ├── test-plan.md
        │   ├── analytics-events.md
        │   ├── threat-model.md       ← solo si §6 compliance ≠ none
        │   ├── cost-estimate.md
        │   ├── build-order.md
        │   └── api-contract.yaml     ← solo Web / Flutter con backend
        └── .claude/
            ├── skills/               ← slash commands
            └── agents/               ← subagentes con modelo asignado
```

## Placeholders

El spec generator reemplaza estos tokens en cada archivo antes de escribirlo:

| Placeholder | Origen en el SPEC.md |
|---|---|
| `{{PROJECT_NAME}}` | título |
| `{{PROJECT_TYPE}}` | header (Flutter mobile / Spreadsheet tool / Web application) |
| `{{WORKING_LANGUAGE}}` | header (idioma de Fase 0) |
| `{{VISION}}` | §1 frase de visión |
| `{{PERSONAS_SUMMARY}}` | §3 lista compacta `nombre — rol — goal` |
| `{{JOURNEYS}}` | §4 títulos de journeys |
| `{{MVP_FEATURE_IDS}}` | §5 IDs con priority=MVP |
| `{{FEATURE_TABLE}}` | §5 tabla completa |
| `{{NON_FUNCTIONAL}}` | §6 línea por requisito |
| `{{TECH_STACK}}` | §7 stack elegido |
| `{{INTEGRATIONS}}` | §7 integraciones |
| `{{LOOK_AND_FEEL}}` | §8 mood + refs + tone |
| `{{GOVERNANCE_BLOCK}}` | §9 bloque del tipo |
| `{{COMPLIANCE_REGIME}}` | §6/9 GDPR/HIPAA/SOC 2/none |
| `{{SUCCESS_METRICS}}` | §10 métricas 30/90 días |
| `{{HARD_CONSTRAINTS}}` | §1 Hard constraints subsection (Phase 0.5) |
| `{{BUDGET}}` | §1 Hard constraints → budget cap |
| `{{DEADLINE}}` | §1 Hard constraints → deadline |
| `{{SCARIEST_MVP_FEATURE}}` | §5 row marked 🚨 build first (Phase 3) |
| `{{RACI_RESPONSIBLE}}` | §9 RACI → Responsible role |
| `{{RACI_ACCOUNTABLE}}` | §9 RACI → Accountable role |
| `{{PERSONA_EVIDENCE}}` | §3 evidence-basis label |
| `{{PROJECT_SLUG}}` | kebab-case slug from project name |
| `{{TODAY}}` | ISO date when rendering happens |
| `{{MVP_FEATURE_COUNT}}` | count of §5 rows with priority=MVP |

## Catálogo

### Skills (22)

Discovery: `spec-revise`, `spec-validate`, `spec-status`, `spec-diff`
Quality gates: `stress-test-spec` (pre-v1.0), `risk` (ongoing), `threat-model`, `api-contract`, `mockup-feedback`
Pre-dev: `mockup` ← navigable HTML POC of the MVP, runs before `/implement`
Development: `implement`, `test`, `review`, `ship`, `design-tokens`
Maintenance: `bug`, `postmortem`, `usage-report`, `spec-evolve`, `dep-update`, `docs-sync`
Meta: `bundle-refresh`

### Agentes (16 entregados por proyecto; type-specific solo el que aplica)

| Carpeta | Agente | Modelo |
|---|---|---|
| discovery | `spec-drift-detector` | claude-opus-4-7 |
| discovery | `persona-prober` | claude-sonnet-4-6 |
| discovery | `mvp-scope-guard` | claude-haiku-4-5-20251001 |
| quality | `spec-stress-tester` | claude-opus-4-7 |
| quality | `risk-tracker` | claude-sonnet-4-6 |
| quality | `threat-modeler` | claude-opus-4-7 |
| quality | `api-contract-author` | claude-sonnet-4-6 |
| quality | `mockup-feedback-collector` | claude-sonnet-4-6 |
| flutter | `flutter-build-doctor` | claude-sonnet-4-6 |
| flutter | `a11y-flutter-auditor` | claude-sonnet-4-6 |
| web | `a11y-web-auditor` | claude-sonnet-4-6 |
| web | `seo-checker` | claude-sonnet-4-6 |
| spreadsheet | `formula-auditor` | claude-opus-4-7 |
| development | `mockup-builder` | claude-sonnet-4-6 |
| development | `feature-implementer` | claude-sonnet-4-6 |
| development | `test-author` | claude-sonnet-4-6 |
| development | `code-reviewer` | claude-opus-4-7 |
| development | `security-reviewer` | claude-opus-4-7 |
| development | `design-translator` | claude-sonnet-4-6 |
| development | `migration-planner` | claude-opus-4-7 |
| development | `e2e-flow-builder` | claude-sonnet-4-6 |
| maintenance | `bug-hunter` | claude-sonnet-4-6 |
| maintenance | `regression-watcher` | claude-sonnet-4-6 |
| maintenance | `dep-updater` | claude-haiku-4-5-20251001 |
| maintenance | `usage-analyzer` | claude-opus-4-7 |
| maintenance | `spec-evolution-advisor` | claude-opus-4-7 |
| maintenance | `incident-postmortem` | claude-opus-4-7 |
| maintenance | `doc-keeper` | claude-haiku-4-5-20251001 |
| maintenance | `support-triage` | claude-haiku-4-5-20251001 |

Total agentes en cualquier bundle entregado: 3 discovery + 5 quality + 1 type-specific group + 8 development + 8 maintenance = **~25 agentes** (varía según tipo).

## Renderizado y refresh

- Al entregar: el spec generator escribe los archivos reemplazando placeholders.
- Al hacer `/spec-revise` que afecte personas, features, stack o governance: invocar `/bundle-refresh` para re-emitir solo los archivos cuyos placeholders cambiaron.
- Cada archivo declara en su frontmatter `spec-fields:` con la lista de placeholders que consume, para que `/bundle-refresh` decida qué regenerar.
