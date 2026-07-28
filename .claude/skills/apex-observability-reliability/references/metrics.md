# Metrics

## Scope
Time-series data about system behavior: counters, gauges, histograms, and dimensional (tagged) metrics for dashboards and alerting.

## Core principles
- Counter (increment-only): total requests, total errors — useful for rates (requests/sec) and error ratios; never reset a counter.
- Gauge (point-in-time value): memory usage, active connections, queue depth — can go up or down; reset on restart.
- Histogram (distribution): request latency, response size — buckets show percentiles (p50, p99); great for understanding tails.
- Cardinality (unique label combinations) must be bounded; avoid high-cardinality tags (user ID, request UUID); instead use low-cardinality tags (service, method, status code).
- Dimensionality (label names and values) determines query power; "http_request_duration_seconds{service='api', method='GET', status='200'}" is more queryable than a flat "api_get_ok_latency_ms".

## Apex practices
- Use Prometheus exposition format (even if using StatsD or others) for consistency; most platforms support it.
- Track business metrics (conversions, revenue, user signups) alongside technical metrics (latency, errors, CPU).
- Set up recording rules (pre-computed aggregations) for expensive queries; Prometheus' TSDB stores both raw and aggregated data.
- Use histogram buckets aligned with SLOs: if your SLO is "99% of requests < 500ms", have buckets at 100ms, 250ms, 500ms, 1000ms.

## Pitfalls
- Cardinality explosion: logging every user ID as a label; instead, count "total_users_active" as a gauge or "requests{user_segment='vip'}" with a small set of segments.
- Histograms with default buckets (exponential) that don't align with SLOs; your p99 bucket might be [500ms, 1000ms] even though you care about 400ms.
- Metrics without labels; "request_count" is useless, but "request_count{service='api', endpoint='/users'}" is actionable.

## Tools & references
Prometheus (TSDB), Grafana (dashboards), StatsD (simple metrics), Datadog (hosted), InfluxDB (time-series DB), OpenTelemetry metrics API, histogram bucket selection (Red Hattics podcast on performance), cardinality management (Prometheus relabel rules).
