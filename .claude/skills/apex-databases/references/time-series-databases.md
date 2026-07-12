# Time-Series Databases

## Scope
Storing and querying timestamped metrics (CPU, memory, temperature, sensor readings). Compression, downsampling, and retention policies. InfluxDB, Prometheus, TimescaleDB, and column-oriented formats.

## Core principles
- Time-series data is append-only (writes are timestamped observations, rarely edited) and high-volume (millions of points per second). Row-oriented databases are inefficient; time-series DBs use column-oriented storage (compress similar values, vectorize computation).
- Retention policies are built-in: keep high-resolution data for 7 days, downsampled hourly for a year. Downsampling (aggregating minute-level to hourly) saves storage at the cost of lost granularity.
- Time-series queries are predictable: "metrics for this host over this time range," often with aggregations (sum, average, max). Most queries scan forward in time, not random access. Sequential I/O dominates.
- Tags (indexed dimensions: host, service, region) enable efficient filtering; fields (values: CPU%, memory MB) are stored but not indexed. Querying by tag is fast; scanning all fields is slow. Balance cardinality carefully (too many unique tags = index explosion).
- Compression is critical: 100-byte raw data points become 1-byte compressed (100x gains) using delta-of-delta encoding (small differences between successive timestamps compress well) and XOR floating-point compression.

## Apex practices
- Use a time-series DB (InfluxDB, Prometheus, TimescaleDB) for metrics, not a general database. The specialized indexing and compression save 10-100x storage and query cost.
- Set retention policies to balance storage and retrospective analysis: high-resolution (1s) for 7 days, medium-resolution (1m) for 30 days, low-resolution (1h) for a year.
- Tag cardinality matters: avoid unique tags per request (request_id, user_id) as tags; store these as fields or not at all. Unique tags explode the index.
- Use downsampling and pre-aggregation for common queries (daily summary, percentile calculations). Compute once (nightly) and cache the results, not on-the-fly.

## Pitfalls
- Storing every attribute as a tag to "enable filtering": high cardinality tags (millions of unique values per tag) cause out-of-memory index and slow queries.
- Not setting retention policies, and the database grows without bound until disk is full.
- Querying too far back in time (months of raw data) without downsampled data; slow queries and massive data transfer.

## Tools & references
InfluxDB documentation (retention, downsampling, InfluxQL/Flux), Prometheus (time-series DB for metrics), TimescaleDB (PostgreSQL extension), "The Art of Monitoring" (Ligus), OpenTelemetry for instrumentation.
