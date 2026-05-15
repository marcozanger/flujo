# Analytics events — {{PROJECT_NAME}}

Single source of truth for what the product tracks. Implement events **with the feature**, not in a separate analytics phase.

**Provider:** *(from §7 — PostHog / Amplitude / Mixpanel / Plausible / GA4 / custom)*
**PII policy:** *(no PII in event properties; user.id is hashed if {{COMPLIANCE_REGIME}} requires)*

## Events

| Event name | Trigger | Properties | Persona | Tied to metric (§10) |
|------------|---------|------------|---------|----------------------|
| `signup_started` | User opens signup form | `source`, `referrer` | All | 30d activation funnel |
| `signup_completed` | Email verified | `time_to_complete_s`, `persona_type` | All | 30d activation rate |
| `feature_X_used` | First successful use | `feature_id`, `outcome` | P1, P2 | Feature adoption |

*(Fill from §10 success metrics. Every metric needs at least one event that measures it. Every event needs a trigger that's unambiguous to implement.)*

## Funnels

```
landing_view → signup_started → signup_completed → activation_completed
```

## Naming convention

- Snake_case, verb-noun (`order_placed`, not `placeOrder`).
- Past tense for events that already happened (`signup_completed`), present for views (`landing_view`).
- Avoid PII in event name or properties — `user_signup` not `user_signup_jane@example.com`.

## Implementation rule

Every PR that adds a §5 feature must also add the matching event(s). The `/review` skill checks this.
