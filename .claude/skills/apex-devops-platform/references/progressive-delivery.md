# Progressive Delivery

## Scope
Deploying changes gradually with automated validation and rollback: canary, blue-green, A/B testing, and feature flags.

## Core principles
- Deploy to a subset first (canary), measure signals (latency, errors, custom metrics), compare to baseline, rollback if degradation is detected.
- Gradual rollout decouples deployment from change — you can deploy infrastructure early and switch live traffic later via flags or load balancing.
- Automated validation is mandatory; manual smoke testing is theater — define metrics that predict user impact (not just uptime), alert if they degrade.
- Rollback must be automatic and fast — if you're waiting for a human to notice and execute a rollback, your SLO is already broken.
- Feature flags enable kill switches and A/B testing; use them for risky changes, but remove them after launch or they become technical debt.

## Apex practices
- Use traffic splitting at the load balancer or service mesh layer (Istio, Linkerd) for canary — weighted routing to pods with different versions lets you do instant rollback.
- Compare canary metrics against a baseline (production metrics before the change) using statistical tests — avoid false positives from normal variance.
- Automate the decision: if error rate increases >5% or latency increases >20%, rollback immediately; require human approval to continue if signals are ambiguous.
- Combine flags and infrastructure canaries: use flags to disable problematic features, use infrastructure canaries to validate at scale before rolling out globally.

## Pitfalls
- Defining "success" as "no crashes" — a degraded service that stays online is worse than a fast rollback; measure actual user impact (conversion, latency percentiles).
- Canary without rollback automation (requires manual intervention) — by the time a human notices and acts, it's too late.
- Feature flags never removed (accumulate to thousands) — they become unmaintainable and create permutation explosion in testing.

## Tools & references
ArgoCD Rollout, Flagger, Spinnaker, LaunchDarkly for flags, Prometheus for metrics, Grafana for alerting, "Accelerate" by Forsgren et al.
