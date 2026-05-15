---
name: ship
description: Pre-release checklist for a {{PROJECT_TYPE}}. Use before a release/store submission/sheet handoff. Type-specific items derived from §9 governance.
spec-fields: [PROJECT_TYPE, GOVERNANCE_BLOCK, NON_FUNCTIONAL, SUCCESS_METRICS]
---

# /ship

Final go/no-go checklist before release. Type-specific.

## What to do
Read `SPEC.md` §9 Governance and §6 Non-functional. Run the matching checklist below.

### If `{{PROJECT_TYPE}}` = Flutter mobile
- [ ] Min iOS / Android targets met (from §9)
- [ ] All declared permissions justified in code
- [ ] App Store privacy nutrition labels filled
- [ ] Play Data Safety form filled
- [ ] Crash reporting SDK configured
- [ ] Forced-update path tested
- [ ] Icons & splash assets at all required sizes

### If `{{PROJECT_TYPE}}` = Web application
- [ ] Hosting target deployed and reachable
- [ ] Auth flow tested end-to-end for each role
- [ ] Browser support matrix verified (§9)
- [ ] WCAG 2.1 AA (or stated target) passes
- [ ] SLA monitoring in place
- [ ] Error tracking configured
- [ ] SEO/SSR if required

### If `{{PROJECT_TYPE}}` = Spreadsheet tool
- [ ] Master copy versioned and named per convention
- [ ] Protected ranges set on all formula cells
- [ ] Audit trail (revision history / Apps Script log) enabled
- [ ] Handoff doc written (see `/docs-sync`)
- [ ] Restore plan documented and tested
- [ ] Owner for ongoing maintenance named in §9

## Output
Checklist with status per item in **{{WORKING_LANGUAGE}}**, plus a single sentence: *"Ready to ship / Not ready — blockers: <list>."*
