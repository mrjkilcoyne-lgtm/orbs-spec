# Cloud Monitoring & Observability

## Scope
Tracking system health, performance, and cost: metrics, logs, traces, alerts, and dashboards.

## Core principles
- Observability (metrics, logs, traces) is your window into what's happening — without it, you're blind to problems until customers report them.
- Metrics (quantitative signals: request count, latency, errors) are cheap to store and fast to query; logs (narrative) are expensive to store but provide context.
- Traces connect requests across services; essential for microservices debugging but also expensive at scale.
- Alerts should predict problems (high latency predicts errors) not report them after the fact; alert on leading indicators.
- Retention matters: keep high-resolution metrics for 1-4 weeks, low-resolution (aggregated) for longer, logs for compliance periods.

## Apex practices
- Use the USE method (Utilization, Saturation, Errors) to pick metrics; avoid "stuff that might be useful" which creates noise.
- Implement structured logging (JSON, key-value pairs) so logs are searchable without full-text regex matching.
- Use distributed tracing (OpenTelemetry) to understand request flows; sample aggressively (1% or less) to keep costs down.
- Build dashboards for on-call operators (what do they need to know in an incident?) not for executives (use business metrics).

## Pitfalls
- Alert on metrics with no runbook (page the on-call engineer with "CPU is high" and no action plan) — every alert needs a runbook.
- Using aggregated metrics only (average latency hides P99, which is what users experience) — track percentiles (P50, P95, P99).
- Logs in unstructured format (grep and regex only, slow, error-prone) — use structured logging from the start.

## Tools & references
Prometheus for metrics, ELK (Elasticsearch, Logstash, Kibana) or Loki for logs, Jaeger for traces, OpenTelemetry for instrumentation, Grafana for dashboards, PagerDuty for alerting.
