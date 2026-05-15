---
name: api-contract
description: Generate or update docs/api-contract.yaml (OpenAPI sketch) from SPEC.md §5 + §4 journeys. Use at spec time for Web/Flutter projects with a backend, and after any §5 change.
spec-fields: [FEATURE_TABLE, JOURNEYS, TECH_STACK, PROJECT_TYPE]
---

# /api-contract

Spawn `api-contract-author` agent (Sonnet 4.6) to draft or refresh `docs/api-contract.yaml`.

## When to use
- At spec delivery if `{{PROJECT_TYPE}}` ∈ {Web, Flutter} and the app has a backend.
- After `/spec-revise §5` (new features → new endpoints).
- Before `/implement` on a backend-touching feature, to lock the contract first.

## What to do

1. Read §5 (features), §4 (journeys), §7 (stack — for auth/error conventions).
2. For each MVP feature that implies a backend call, derive:
   - HTTP method + path
   - Request shape (auth header, body)
   - Response shapes (200/4xx/5xx)
   - Tied feature ID
3. Use idiomatic REST or whatever §7 specifies (GraphQL, tRPC, gRPC).
4. Emit valid OpenAPI 3.1 YAML.
5. **Don't** lock in details that aren't in the spec — leave `description: TBD` and reference §12 if a shape is uncertain.

## Output

`docs/api-contract.yaml` + a summary in **{{WORKING_LANGUAGE}}**:
- Endpoints added/changed
- TBDs needing user input
- Suggested next: open the contract with stakeholders before `/implement` on backend features

## Constraints

- Sketch, not authoritative. Real implementation may evolve the contract; that triggers a refresh via this skill.
- Don't invent auth schemes — pull from §7.
