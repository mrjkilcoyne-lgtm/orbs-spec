# SLOs and SLIs

## Scope
Defining and measuring service reliability: service-level objectives (SLOs), indicators (SLIs), and tracking against error budgets.

## Core principles
- SLO (goal) is a statement: "99.9% of requests will succeed and complete in < 100ms per calendar month."
- SLI (indicator) is the measurement: actual success rate, actual latency percentile; it's what you actually achieve.
- Error budget is 1 - SLO: if your SLO is 99.9%, your budget is 0.1% of requests (or time) that can fail or be slow; once spent, stop shipping features and fix reliability.
- SLOs must be achievable and meaningful: if you promise 99.99% availability, you need < 43 seconds of downtime per year; that's hard and expensive.
- SLIs must be observable: you can't have an SLO for "customer satisfaction" unless you measure it (NPS, surveys); instead, measure "checkout success rate" as a proxy.

## Apex practices
- Start with achievable SLOs (95-99% availability) and tighten them as the system matures; 99.99% requires serious engineering.
- Track multiple SLIs: request success ratio, latency (p99), and freshness (staleness of cached data).
- Align SLOs with user expectations: mobile users tolerate 2-second latencies, but internal dashboards need < 500ms.
- Build error budget burn dashboards: if you're on track to burn your annual budget in 3 months, pause features and fix reliability.

## Pitfalls
- Choosing unrealistic SLOs (99.99% is extremely hard); undershooting and then trying to change is demoralizing.
- Treating SLO as a ceiling instead of a guardrail; if you're well above SLO (99.99% when targeting 99%), you're overbuilding.
- Not including human time in availability calculations; a service is not "available" if it requires manual intervention to recover.

## Tools & references
Google's SRE Book (SLO chapter), Error Budget Calculator (Google), Datadog SLO tracking, New Relic SLI/SLO, Lightstep, PagerDuty (error budget integration), SLO spec (SLOGI working group).
