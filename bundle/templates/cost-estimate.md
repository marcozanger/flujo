# Cost estimate — {{PROJECT_NAME}}

**Horizon:** 12 months from launch
**Last updated:** {{TODAY}}
**Refresh trigger:** any `/spec-revise §7` (stack change) or §6 (scale change).

Estimate, not contract. Real costs will differ — track actuals monthly and refresh this doc quarterly.

## Monthly cost — steady state

| Category | Service | Plan | Cost / month | Notes |
|----------|---------|------|--------------|-------|
| Hosting | Vercel / Fly / Cloud Run | Hobby → Pro | US$0 → 20 | Scales with traffic |
| Database | Supabase / Neon / RDS | Free → S | US$0 → 25 | Free tier covers MVP usage |
| Auth | Clerk / Auth0 / Supabase Auth | Free tier | US$0 | < 10k MAU |
| Payments | Stripe | N/A | 2.9% + 30¢/txn | Variable; not flat |
| Email | Resend / Postmark | Free → S | US$0 → 15 | 3k → 10k emails |
| Analytics | PostHog cloud | Free → S | US$0 → 50 | Above 1M events |
| Error tracking | Sentry | Team | US$26 | 50k errors/month |
| Domain + SSL | Cloudflare | — | US$12 / year | |
| Monitoring | UptimeRobot | Free | US$0 | 50 monitors |
| **Total (low / high)** | | | **US$XX / US$YYY** | |

*(Fill from §7 stack + §6 scale targets — replace placeholders with the actual chosen services.)*

## One-time setup costs

| Item | Cost | Notes |
|------|------|-------|
| Design tokens / brand work | US$0–5k | If §8 brand assets = "none" |
| Legal review (ToS, Privacy) | US$0–2k | Required if {{COMPLIANCE_REGIME}} ≠ none |
| Security audit | US$0–10k | Recommended before public launch if compliance ≠ none |

## Cost-of-scale curves

- **1k → 10k users:** mostly flat (free tiers cover)
- **10k → 100k users:** ~+US$200–500/month (auth tier upgrade, DB tier upgrade)
- **100k+ users:** custom pricing on auth/DB/email; budget US$2–5k/month and re-evaluate

## Cost vs §1 budget cap

- Budget cap from §1: {{BUDGET}}
- Projected 12-month run cost: US$XXX
- Buffer / overrun risk: …

## Optimization opportunities

- Move from SaaS-X to OSS-Y at scale Z
- Consolidate observability stack (Sentry + PostHog overlap)
