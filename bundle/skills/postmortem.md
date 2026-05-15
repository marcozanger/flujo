---
name: postmortem
description: Write an incident postmortem anchored on SPEC.md success criteria and journeys. Use after a production incident is resolved.
spec-fields: [JOURNEYS, NON_FUNCTIONAL, SUCCESS_METRICS]
---

# /postmortem

Arguments: `<incident-id-or-short-title>`.

## What to do
1. Gather: timeline, detection, mitigation, resolution. Ask the user for what they have.
2. Identify which §4 journey(s) were broken and which §6 non-functional target(s) were violated (latency, availability, etc.).
3. Spawn `incident-postmortem` agent for root-cause analysis.
4. Write the postmortem with these sections:
   - **Summary** (3–5 lines)
   - **Impact** — personas affected × duration × journey broken
   - **Timeline** — UTC, detection → resolution
   - **Root cause** — from agent
   - **What worked / What didn't**
   - **Action items** — each with owner, severity, and whether it triggers `/spec-evolve`
5. Save as `docs/postmortems/YYYY-MM-DD-<slug>.md`.

## Output
The postmortem doc + a single sentence in **{{WORKING_LANGUAGE}}** flagging action items that warrant a `/spec-evolve`.

## Never
- Assign blame to individuals. Postmortems are blameless — focus on systems and gaps.
