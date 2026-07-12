# Cloud Functions (Serverless)

## Scope
Event-driven, auto-scaling functions: AWS Lambda, GCP Cloud Functions, Azure Functions; scaling, cold starts, and concurrency.

## Core principles
- Serverless functions are billed per invocation and execution time — optimize for short run time and low invocation rate, or costs explode.
- Cold starts (initial invocation latency) are a real issue; provisioned concurrency or reserved instances reduce cold-start latency.
- Functions are ephemeral and stateless; store state in databases or object storage, not on the filesystem.
- Concurrency is the resource limit — a function has max concurrent executions; requests beyond that are throttled or queued.
- Timeout (function must complete within X seconds) and memory (CPU scales with memory) are the configuration levers.

## Apex practices
- Use serverless for event-driven workloads (webhooks, scheduled jobs, message processing) not for high-frequency, low-latency operations.
- Implement connection pooling (databases, HTTP clients) — creating a new connection per invocation is expensive and slow.
- Use provisioned concurrency for critical functions to avoid cold starts; use on-demand for non-critical workloads.
- Implement idempotent handlers (functions may be invoked multiple times for the same event) using idempotency keys.

## Pitfalls
- Using serverless for compute-heavy workloads (long-running, high CPU) — the per-second billing makes it expensive.
- No cold-start testing (production users hit cold starts after deployment or quiet periods) — use production traffic or synthetic tests.
- Functions that call other functions (expensive cascades) — optimize the call graph or batch operations.

## Tools & references
AWS Lambda, GCP Cloud Functions, Azure Functions, AWS SAM for infrastructure as code, Serverless Framework, Lambda Layers for dependencies.
