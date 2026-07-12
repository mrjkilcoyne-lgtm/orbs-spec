# OpenTelemetry

## Scope
Standard instrumentation APIs and protocols for logs, metrics, and traces: vendor-neutral integration across observability backends.

## Core principles
- OpenTelemetry (OTel) is a standard for emitting observability data; applications instrument once, and data routes to any backend (Datadog, New Relic, Grafana, Jaeger).
- The OTel SDK handles sampling, batching, and exporting; applications use the API and never touch transport.
- Semantic conventions (standards for attribute names: http.method, http.status_code) enable cross-tool analysis and correlation.
- No vendor lock-in: if you're using OTel, you can switch backends by changing config, not code.
- Spans link requests across services; logs and metrics are linked through the trace ID and context.

## Apex practices
- Use OTel SDKs (Java, Python, Go, Node) from the start; retrofitting instrumentation is expensive.
- Instrument critical paths: HTTP handlers, database queries, external API calls, and business logic checkpoints.
- Set up context propagation (trace ID headers) from the HTTP handler down through middleware and libraries automatically via OTel.
- Export to a backend (Jaeger, Tempo, Datadog) over OTLP (OpenTelemetry Protocol) for standardized ingestion.

## Pitfalls
- Over-instrumentation that generates too much data (cardinality explosion, high costs).
- No sampling; without sampling, you'll generate terabytes of trace data per day in high-traffic systems.
- Not using semantic conventions; custom attribute names make cross-team analysis impossible.

## Tools & references
OpenTelemetry (CNCF), Semantic Conventions (OTel spec), OTLP (protocol), Jaeger (open-source backend), Grafana Tempo (OTel backend), Datadog (OTel-native), New Relic, OTel SDKs (Java, Python, Go, Node.js).
