---
name: start
description: Bootstrap a new requirements-gathering interview from a blank slate. Loads project-instructions.md, sets up internal state, and asks the Phase 0 working-language question. This is the single entry point — use it to begin generating a new SPEC.md + docs/ + .claude/ bundle for a user project.
---

# /start

Single entry point to launch a new interview that produces `SPEC.md` + companion artifacts + `.claude/` bundle for a user project, all written under `projects/<slug>/` (gitignored from this `flujo` repo).

## What to do

1. **Load context.** Read these files to refresh the assistant's role and the system:
   - `project-instructions.md` — full phase definitions, canonical question format, spec template, when-to-stop conditions
   - `bundle/README.md` — placeholder map, catalog of skills/agents, templates
   - `starter-conversation.md` — welcome-message reference *(optional, the /start invocation supersedes it)*

2. **Initialize state.** Track internally throughout the interview:
   - Working language: TBD *(locked in Phase 0)*
   - Project slug: TBD *(set after Phase 1 vision phrase)*
   - Project type: TBD *(Flutter mobile / Spreadsheet tool / Web application — Phase 1)*
   - Output path: `projects/<slug>/` *(materializes at Phase 9)*
   - Current phase: starting Phase 0
   - Completed phases: 0 of 10

3. **Send a short welcome + Phase 0 question.** Mirror the language the user invoked `/start` in. Default to English if unclear. Don't dump the full 9-phase outline — just one line of context and the language question per `project-instructions.md` Phase 0.

4. **Show progress on every phase transition.** At the start of each new phase, emit this 4-line block in the working language — see `project-instructions.md` Operating principles for the full spec:

   ```
   📊 <N>% completo · Phase <X> / 10 — <Phase name>
   ✅ Listas: <completed phase short names>
   🔵 Ahora:  <current phase short name>
   ⬜ Faltan: <remaining phase short names joined with →>
   ```

   Short names + %: Language (0%) · Constraints (10%) · Vision & type (20%) · Personas (30%) · Features & MVP (40%) · NFR (50%) · Stack (60%) · Look & feel (70%) · Governance (80%) · Success (90%) · Delivery (100%).

   Example at the start of Phase 2:
   ```
   📊 30% completo · Phase 2 / 10 — Personas
   ✅ Listas: Language · Constraints · Vision & type
   🔵 Ahora:  Personas
   ⬜ Faltan: Features & MVP → NFR → Stack → Look & feel → Governance → Success → Delivery
   ```

5. **Run phases in order** per `project-instructions.md`. After each reflection-and-confirmation, advance to the next phase **and emit the progress line**.

6. **Hold all output until Phase 9.** Do not write `SPEC.md`, `docs/*`, or `.claude/*` to disk before the interview is confirmed and all "When to stop interviewing" conditions are met.

## Reference

- `project-instructions.md` — system prompt for the interviewer role
- `bundle/templates/` — artifact templates rendered into `projects/<slug>/docs/` at Phase 9
- `bundle/skills/` and `bundle/agents/` — rendered into `projects/<slug>/.claude/` at Phase 9
- `bundle/README.md` — full placeholder map

## Never

- Skip Phase 0 (working language) or Phase 0.5 (hard constraints), even if the user volunteers a vision phrase first. Capture what they said, then return to the phase order.
- Generate `SPEC.md` or any file before reaching Phase 9 with confirmed answers per `When to stop interviewing`.
- Write output outside `projects/<slug>/`.
- Omit the progress line on a phase transition.
