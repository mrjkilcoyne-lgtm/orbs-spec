# Logging

## Scope
Recording discrete events and context from a running system: structured logging, log levels, cardinality, and retention policies.

## Core principles
- Structured logging (JSON, key-value pairs) is superior to unstructured strings; log aggregators (ELK, Datadog, New Relic) cannot parse "something went wrong" but can parse {"error": "timeout", "service": "auth"}.
- Log levels (DEBUG, INFO, WARN, ERROR) should be semantic: ERROR is a user-facing failure, WARN is a recoverable issue, INFO is a state transition, DEBUG is for development.
- Cardinality explosion (too many unique values in a single field) makes logs unsearchable; avoid logging raw user IDs, request UUIDs, or SQL queries as high-volume fields.
- Sampling (logging 1% of requests in high-volume services) reduces cost but risks losing the error log you need; sample based on outcome (log errors 100%, success 1%) not randomly.
- Retention (how long logs are kept) is a cost-reliability tradeoff; 30 days is common, but compliance (GDPR, HIPAA) may require longer or shorter.

## Apex practices
- Use structured logging from application startup: every log line includes request ID (for correlation), service name, version, and environment.
- Add context before logging errors (what operation, what user, what resource); one-line errors are useless for debugging.
- Use log aggregators (Datadog, New Relic, Splunk, Loki) with full-text search and dashboards; grepping production server logs is archaeology.
- Implement cost-aware sampling in the logging library itself, not in the aggregator; send only what you'll keep.

## Pitfalls
- Logging unencrypted secrets (API keys, passwords, tokens); log scrubbing (finding and redacting secrets) is hard and error-prone.
- Logging at the wrong level (ERROR for every user input error instead of WARN or INFO).
- Synchronous logging that blocks on disk I/O; use async loggers (Logback, Bunyan) and batch writes.

## Tools & references
Structured logging libraries (logrus, Pino, Bunyan, log4j2), ELK Stack (Elasticsearch, Logstash, Kibana), Datadog, Splunk, Loki, log retention calculators, GDPR-compliant logging, cardinality tools (Datadog cardinality explorer).
