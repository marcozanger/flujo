---
name: mockup-feedback
description: Capture stakeholder reactions to the /mockup in structured form and turn them into spec change candidates. Use after each stakeholder review session.
spec-fields: [JOURNEYS, PERSONAS_SUMMARY, FEATURE_TABLE]
---

# /mockup-feedback

Spawn `mockup-feedback-collector` agent (Sonnet 4.6).

## When to use
- Immediately after a stakeholder review of the `mockup/`.
- Before `/implement` if mockup changed since last review.

## What to do

1. Ask the user to paste raw notes from the review (their notes, transcripts, written feedback, screenshots with comments).
2. Spawn `mockup-feedback-collector`. It will:
   - Classify each comment: **positive** / **friction** / **don't-understand** / **scope-question** / **off-topic**
   - Map to specific mockup screens / journeys / features
   - Identify clusters (the same friction mentioned by ≥2 people)
   - Distinguish **mockup-only fixes** (e.g. "button position") from **spec-impacting fixes** (e.g. "we need a step we forgot")
3. Save the structured feedback at `mockup/feedback/<YYYY-MM-DD>-session.md`.
4. For spec-impacting items, propose `/spec-revise` candidates with quotes.

## Output

In **{{WORKING_LANGUAGE}}**:
```
# Mockup feedback session — YYYY-MM-DD (N participants)

## Themes
- [cluster] Friction on J2 step 3 (4 mentions) — modal too tall
- [cluster] Don't-understand on terminology "X" (3 mentions)

## Mockup-only fixes (apply with next /mockup --refresh)
- …

## Spec-impacting (proposed /spec-revise)
- §5 F4 — terminology change "Sync" → "Update" — supported by quote: "I keep thinking sync means cloud sync"

## Positive signals
- Persona Marina (P1) completed J1 in <30s without help (good for §10 baseline)
```

## Constraints

- Preserve user voice. Quote feedback verbatim when proposing a `/spec-revise`.
- Don't bundle mockup-only + spec-impacting in one PR. They're different change classes.
