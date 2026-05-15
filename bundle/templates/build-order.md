# Build order — {{PROJECT_NAME}}

**Principle:** retire the **biggest risk first**, not the easiest feature first. The feature marked `🚨 build first` in §5 (from Phase 3 "scariest feature" question) goes #1.

**Refresh:** `/bundle-refresh` after any `/spec-revise §5` priority change.

## Recommended order

| # | Feature | Why this position | Blocks |
|---|---------|-------------------|--------|
| 1 | 🚨 {{SCARIEST_MVP_FEATURE}} | Highest risk — retire it before investing in the rest | All MVP features depend on this proving feasible |
| 2 | Auth / signup | Foundation; every journey needs it | All UI work |
| 3 | F-data-model-core | Schema must exist before features that read/write | F3, F4, F5 |
| 4 | F3 (MVP) | Primary value-driver per §1 vision | F7 reporting |
| 5 | F4 (MVP) | Tied to §10 success metric | — |
| … | … | … | … |

*(Fill from {{FEATURE_TABLE}} respecting the 🚨 marker.)*

## Sequencing rules

1. **Risk before value.** Build the scariest feature first to learn cheap.
2. **Foundation before features.** Auth, data model, and one journey end-to-end before parallelizing.
3. **One vertical slice first.** Get *one* feature shipped end-to-end (UI → API → DB → tests → mockup-verified) before starting #2.
4. **Admin tooling alongside, not after.** From Phase 3 admin tooling question — if MVP-priority, sequence with the first feature it supports.
5. **Don't batch fast features.** Resist the temptation to do 5 small features in one sprint; one-by-one keeps reviews honest.

## When to revise

- A higher-risk feature is discovered → bump it up
- A blocking dependency is found → resequence
- The scariest feature is proven (or killed) → re-evaluate #1

Each revision = `/spec-revise §5` then `/bundle-refresh`.
