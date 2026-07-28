# On-Call

## Scope
Structuring on-call rotations, escalations, and runbooks to minimize response time and engineer burnout.

## Core principles
- On-call is an interruption; frequent interruptions (paging > 2x/week per engineer) cause burnout and turnover; sustainable systems page < 1x/week on average.
- Escalation protocols (who to call if the primary doesn't acknowledge in 5 minutes) prevent one person becoming a bottleneck.
- On-call schedules can be primary-backup (one person bears the load, backup handles escalations) or round-robin (faster response, but more interruption distribution).
- Runbooks (playbooks for common incidents) reduce mean-time-to-resolution (MTTR) by 10-50x; an engineer shouldn't have to diagnose from scratch at 3am.
- Context handoff (metrics, logs, traces, recent changes) delivered with the alert reduces time to diagnosis.

## Apex practices
- Limit on-call shifts to 1 week; burnout increases dramatically after 3+ weeks.
- Require a runbook for every alert; if you can't write a runbook, the alert is probably not actionable.
- Measure on-call metrics (MTTR, page volume per engineer, false alert rate) and optimize regularly.
- Give on-call engineers high context: send the alert with dashboards, recent deployments, and affected customers.

## Pitfalls
- On-call on top of day job (no backfill) leads to burnout; schedule on-call for people on-call, not people coding.
- Vague escalation paths; if Alice can't handle an incident, who does she call? Without clear escalation, 30+ minutes are lost.
- Punishing on-call engineers for incidents; on-call is supposed to catch bugs that QA missed, not a performance metric for engineers.

## Tools & references
PagerDuty, Opsgenie, OnCall (Grafana), Ilert, Incident.io, on-call burnout research (VictorOps), Google SRE runbook templates, escalation policy design.
