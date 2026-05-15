---
name: threat-model
description: Generate or update docs/threat-model.md — STRIDE-based threat modeling tied to §6 compliance regime. Use at spec time and whenever §5/§6/§7 changes affect attack surface.
spec-fields: [FEATURE_TABLE, NON_FUNCTIONAL, COMPLIANCE_REGIME, TECH_STACK]
---

# /threat-model

Spawn `threat-modeler` agent (Opus 4.7) to build or refresh STRIDE for **{{PROJECT_NAME}}**.

## When to use
- At spec delivery if §6 `{{COMPLIANCE_REGIME}}` ≠ none.
- After `/spec-revise` on §5 (new features = new attack surface), §6 (new compliance), or §7 (new stack/integration).
- Annually as a sanity refresh.

## What to do
1. Read §3 personas (who attacks vs who's attacked), §5 features (assets to protect), §6 compliance, §7 stack/integrations.
2. For each major component (trust boundary), run STRIDE:
   - **S**poofing — identity attacks
   - **T**ampering — integrity attacks
   - **R**epudiation — non-deniability gaps
   - **I**nformation disclosure — leakage
   - **D**enial of service — availability
   - **E**levation of privilege — authz bypass
3. For each threat: rate likelihood (L/M/H), impact (L/M/H), and propose mitigation. Tie to compliance clauses where relevant.
4. Write `docs/threat-model.md` as a structured table.

## Output

Markdown in **{{WORKING_LANGUAGE}}**:
- Trust boundary diagram (Mermaid)
- STRIDE table per boundary
- Mitigations mapped to existing §5 features and any new ones needed (these become candidates for `/spec-revise §5`)
- Top 5 threats summary

## Constraints

- Don't theatre-threat. If a category doesn't apply (e.g. no auth = no privilege escalation), say so explicitly.
- Communicate in **{{WORKING_LANGUAGE}}**.
