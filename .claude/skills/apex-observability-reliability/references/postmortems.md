# Postmortems

## Scope
Analyzing incidents blameless: root cause, contributing factors, timeline, and action items to prevent recurrence.

## Core principles
- Blameless postmortems ask "why?" five times (Five Whys): surface the systemic issue, not the human error (the error is a symptom, not the disease).
- Root cause is often a missing check or test; "the engineer didn't notice the typo" is a symptom, the root cause is "no code review and no tests for config syntax."
- Contributing factors are conditions that made the incident likely (alert thresholds were too permissive, runbook was outdated, context was missing).
- Action items must be concrete and assigned: "improve observability" is vague, "add latency alert at p99 > 200ms with runbook" is actionable.
- Postmortems should be written in the first 24-48 hours while details are fresh; waiting a week leads to forgotten context.

## Apex practices
- Write postmortems in a blameless voice: "the deployment was missing a database migration" not "the engineer forgot the migration."
- Separate action items by priority (fix today vs. improve next quarter) and by ownership (one person per action item).
- Publish postmortems internally (all engineers read them) to distribute learning; secrets and internal politics can be redacted.
- Link postmortem action items to tickets and track completion; untracked action items become tech debt.

## Pitfalls
- Writing postmortems to justify the incident ("it was very hard to predict"); learn instead of explaining.
- Assigning action items to "the team" instead of a person; action items without owners don't get done.
- Concluding that the fix is "better monitoring" when the root issue is a missing test; monitor the outcome, but fix the root cause.

## Tools & references
Blameless (postmortem SaaS), Google Postmortem template, Etsy's John Allspaw on blameless culture, incident-post-mortem (GitHub template), Incident.io postmortem integration, Five Whys technique.
