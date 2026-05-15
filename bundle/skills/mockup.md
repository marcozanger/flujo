---
name: mockup
description: Build a navigable HTML mockup/POC of the MVP before writing real code. Use right after SPEC.md is delivered and before /implement. Lets stakeholders test navigation and look & feel without any backend.
spec-fields: [JOURNEYS, MVP_FEATURE_IDS, FEATURE_TABLE, PERSONAS_SUMMARY, LOOK_AND_FEEL, PROJECT_TYPE]
---

# /mockup

Generate a static, navigable HTML POC that covers the MVP journeys from `SPEC.md` §4.

The goal is to **validate navigation + look & feel + journey coherence early**, before any backend or framework work. Output is plain HTML/CSS (and minimal JS for nav), works offline, no build step.

## Arguments
- *(none)* — mock every §4 MVP journey
- `--journey <name>` — mock a single journey
- `--refresh` — regenerate after a `/spec-revise` on §3 / §4 / §5 / §8

## What to do

1. Read `SPEC.md` §3 (personas), §4 (journeys), §5 (MVP features only), §8 (look & feel), and `{{PROJECT_TYPE}}`.
2. If `/design-tokens` hasn't been run yet, run it first so the mockup uses real tokens.
3. Spawn `mockup-builder` agent. Pass it the journey list and the persona that owns each.
4. Output structure:
   ```
   mockup/
   ├── index.html        ← sitemap with one journey per row
   ├── tokens.css        ← from /design-tokens
   ├── shared/
   │   ├── layout.css
   │   └── nav.js        ← minimal hash router or just <a> links
   └── screens/
       ├── j1-step1.html
       ├── j1-step2.html
       └── …
   ```
5. Each screen page includes a small floating annotation panel (collapsible) showing:
   - Journey name + step number from §4
   - Persona piloting (from §3)
   - §5 feature IDs this screen surfaces
   - What's stubbed vs. what would be live
6. Adapt to `{{PROJECT_TYPE}}`:
   - **Web** — full responsive viewport.
   - **Flutter mobile** — wrap each screen in a phone frame (iPhone/Pixel mock), fixed mobile viewport, touch-friendly tap targets.
   - **Spreadsheet** — render each planned sheet as an HTML `<table>` with sample data, conditional formatting via CSS, sheet tabs at the bottom.

## Output

A summary in **{{WORKING_LANGUAGE}}**:
- Files generated (paths)
- Journeys covered
- Stubs/placeholders that need user input (copy, real sample data, brand logo)
- How to view it locally: `cd mockup && python -m http.server 8080` (or just open `index.html`)
- One line: *"Review the mockup with stakeholders. When approved, run `/implement <FeatureID>` to start building. If something doesn't feel right, run `/spec-revise` on the relevant section first."*

## Constraints

- **Static only.** No real fetches, no framework, no build step. Plain HTML/CSS/JS.
- **MVP scope only.** Don't mock §5 rows priced as `v1.x` or `Later`.
- **Use §8 verbatim.** Mood adjectives, references, brand assets — pull from the spec, don't invent.
- **Sample data must be plausible.** Use names from §3 personas as users; numbers consistent with §10 success metrics.
- Communicate in **{{WORKING_LANGUAGE}}**.
