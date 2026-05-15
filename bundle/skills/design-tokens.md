---
name: design-tokens
description: Export design tokens (color, type, spacing, radius, shadow) from SPEC.md §8 Look & feel. Use once at project start, and again after any §8 revision.
spec-fields: [LOOK_AND_FEEL, PROJECT_TYPE]
---

# /design-tokens

Translate the mood + references + brand assets in §8 into a concrete tokens file.

## What to do
1. Read `SPEC.md` §8.
2. Decide format from `{{PROJECT_TYPE}}`:
   - Web → CSS custom properties + a `tokens.json` for tooling.
   - Flutter → a `ThemeData` extension or `theme_tokens.dart`.
   - Spreadsheet → a "Style guide" sheet with named cell styles.
3. Use brand assets if `binding`; treat references as inspiration if `starting point`; invent conservatively if `none` and surface as TBDs.
4. Generate at minimum:
   - Color: primary, secondary, success/warning/error, surface, text-on-surface, text-on-primary.
   - Type scale: 4–6 sizes with line-heights.
   - Spacing: 4/8/12/16/24/32/48 (or platform convention).
   - Radius: sm/md/lg.
   - Elevation/shadow: 1–3 levels.

## Output
The tokens file + a markdown summary in **{{WORKING_LANGUAGE}}** explaining each choice and which §8 sentence drove it. Anything not derivable from §8 is marked `TBD` and added to §12 via `/spec-revise`.

## Never
- Invent brand colors when §8 names binding assets. Use the assets.
- Use Material/iOS defaults silently when the spec asks for a custom feel.
