# Chaos Engineering

## Scope
Deliberately introducing failures to systems to discover and fix weaknesses before customers experience them.

## Core principles
- Resilience isn't tested, it's engineered — you must trigger failures and observe recovery; if you've never seen a failure mode, you're unprepared for it.
- Blast radius matters — chaos tests should start small (single pod, single region) and expand, not take down production immediately.
- Chaos experiments are repeatable — define the failure, duration, target, and success criteria; run again next week to verify fix and catch regressions.
- Observability is prerequisite — without metrics, logs, and traces, you can't tell if the system recovered correctly or just appeared to work.
- Chaos should improve confidence, not cause outages — run in staging or canary first; production chaos requires sufficient redundancy and safeguards.

## Apex practices
- Start with the steady state (what does normal look like?) then inject faults (latency, errors, pod termination) and verify convergence (does traffic flow again?).
- Run chaos experiments on a regular schedule (weekly, after deployments, on-demand after major changes) so teams practice response and verify remediations.
- Implement abort conditions (if error rate exceeds X%, stop the experiment automatically) to prevent cascading failures.
- Document and share results (which failure modes were discovered, how were they fixed, did they matter?) so the organization learns.

## Pitfalls
- Running chaos experiments that don't match real failure modes (your test fails at 10Mbps latency but production fail at 100ms jitter).
- Chaos without rollback (engineers can't revert the chaos if the system doesn't recover) — implement circuit breakers and manual abort.
- No observability during chaos (discovering problems later in logs is too late) — real-time dashboards that show what's happening during the test.

## Tools & references
Gremlin, Chaos Mesh, Pumba, kube-monkey, "Chaos Engineering" by O'Reilly, PagerDuty Chaos Engineering guide, Netflix Chaos Monkey history.
