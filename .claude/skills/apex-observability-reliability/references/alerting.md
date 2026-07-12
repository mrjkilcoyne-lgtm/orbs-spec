# Alerting

## Scope
Creating and routing alerts from metrics and events to on-call responders; alert tuning, thresholds, and reducing alert fatigue.

## Core principles
- An alert should represent an actionable problem: "CPU is 90%" is not actionable (what should you do?), but "P99 latency is 5 seconds" is (investigate the slowdown).
- Alert fatigue (too many false positives) leads to alert numbness and missed real incidents; every alert that fires is either too sensitive or not useful.
- Alert severity (critical, warning, info) determines routing and escalation; critical pages an on-call engineer, warning creates a ticket for the next day.
- Thresholds must account for normal variation; if your SLO is 99%, alert at 95% to catch degradation early but allow for variance.
- Static thresholds (CPU > 80%) fail in elastic systems; dynamic thresholds (anomaly detection, baseline-relative) are more robust.

## Apex practices
- Write alerts with clear runbooks: "P99 latency breach → check database slow logs → restart max_connections."
- Use service-level monitoring instead of component monitoring when possible: alert on "payment success rate" not "database CPU" (the database might be fine but still cause failures).
- Set alert fatigue budgets: measure false positive rate, aim for < 10% (most alerts are real problems).
- Group related alerts (deduplication, correlation) to reduce noise; if 100 pods are down, fire one "service degraded" alert, not 100 pod alerts.

## Pitfalls
- Alerting on instantaneous values (CPU this second); use windowed averages (CPU over 5 minutes) to tolerate normal variation.
- Escalation that always pages; if a warning is so urgent it needs immediate escalation, make it critical.
- Alerts without clear next steps; "anomaly detected" is useless without telling the responder what to do.

## Tools & references
Prometheus AlertManager, Datadog alerting, New Relic, PagerDuty (alert routing), Opsgenie (escalation), alert fatigue studies (VictorOps 2016), dynamic thresholds (Datadog anomaly detection, Splunk ML Toolkit).
