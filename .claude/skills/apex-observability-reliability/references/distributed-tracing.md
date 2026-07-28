# Distributed Tracing

## Scope
Tracking requests across multiple services and databases: span correlation, trace context propagation, and sampling for scale.

## Core principles
- A trace is a request's path through the system; a span is a unit of work within a service; spans are linked by trace IDs (request correlation).
- Trace context must be propagated across service boundaries (HTTP headers, gRPC metadata, message queues); without this, traces fragment.
- Head-based sampling (deciding to trace at the entry point) is simpler but misses interesting tail requests; tail-based sampling (deciding after seeing the full trace) requires buffering all spans.
- Sampling rates must be balanced: 1% of requests in high-traffic systems = millions of spans/sec; tracing everything is unaffordable, so sampling is mandatory.
- W3C Trace Context (standard header format) is becoming ubiquitous; it's the path to interoperability between tracing systems.

## Apex practices
- Propagate trace ID through all downstream calls (HTTP X-Trace-ID header, gRPC metadata, message queue envelope).
- Use OpenTelemetry SDKs to instrument code; they handle context propagation and sampling automatically.
- Set up tail-based sampling in the collector (sample high-latency or error traces at higher rates) to capture interesting cases.
- Link traces across async work (jobs, webhooks) by passing the trace ID; async work is invisible to request tracing otherwise.

## Pitfalls
- No trace context propagation across services; each service starts a new trace, and the full request flow is invisible.
- Sampling that loses errors; always sample error traces to 100% and adjust success trace rates to stay within budget.
- Trace ID collisions (using predictable IDs like sequential counters); use cryptographically random IDs (128-bit minimum).

## Tools & references
Jaeger (open-source, CNCF), Tempo (Grafana's backend), DataDog APM, New Relic, OpenTelemetry (instrumentation standard), W3C Trace Context (spec), tail-based sampling (Lightstep, Datadog), span attributes (semantic conventions).
