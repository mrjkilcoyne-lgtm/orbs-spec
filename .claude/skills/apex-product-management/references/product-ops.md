# Product Ops

## Scope
The infrastructure enabling product teams to run: roadmap governance, prioritization processes, metrics dashboards, and tools that reduce friction from idea to shipped.

## Core principles
- Product ops is not a team of gatekeepers; it's an enabling function that automates the non-repeatable work (roadmap synthesis, stakeholder alignment, metric calculation) so product managers can focus on decisions.
- The roadmap is the org's shared model of what's happening and why; if the roadmap lives in Jira epics and the CEO's Slack messages disagree, the roadmap is not the roadmap.
- Instrumentation must precede decisions: ship the product telemetry and dashboards first, then run the meeting; "we'll measure it later" means you'll make decisions on vibes.
- Processes scale better than people: a 20-person product org needs documented, repeatable cadences (planning, review, prioritization) or each new PM invents their own.
- The tools (Jira, Figma, Looker, whatever) are dumb pipes; product ops ensures data flows through them consistently (team A tags features with Qx2024, team B tags Fy2024; now the exec dashboard is broken).

## Apex practices
- Implement zero-configuration rollout tracking: every shipped feature lands with a feature flag and A/B test harness so teams don't have to ask permission to measure impact.
- Automate the cadence: calendar holds for planning (first week of quarter), review (third week), and calibration (weekly). Default behavior beats cultural nagging.
- Create a single source of truth for the roadmap (Notion, Amplitude, Vimeo, doesn't matter) that auto-syncs to Jira and calendar; redundant systems cause drift.
- Run monthly prioritization calibrations where teams defend their backlog priorities against company OKRs and each other; visible trade-offs beat hidden politics.

## Pitfalls
- A product ops function that owns the roadmap instead of facilitating product teams' roadmaps; the PM must own the prioritization decision or they check out.
- Metrics dashboards that report vanity numbers (page views, accounts created) instead of outcome metrics (revenue contribution, retention curve, time-to-value).
- Changing the planning process every quarter because someone read a blog post; consistency compounds more than process fidelity.

## Tools & references
Amplitude, Looker, LaunchDarkly (feature flags), ProdPad, Reforge's Product Strategy course, Intercom's "Inside Intercom" on roadmapping, Teresa Torres' "Continuous Discovery Habits."
