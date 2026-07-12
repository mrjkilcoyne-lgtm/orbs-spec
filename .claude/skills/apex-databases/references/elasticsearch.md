# Elasticsearch

## Scope
Search and analytics engine (built on Lucene). Full-text search, aggregations, and time-series (ELK stack: Elasticsearch, Logstash, Kibana). Distributed indexing and querying.

## Core principles
- Elasticsearch is a Lucene-based search engine optimized for text queries (fuzzy matching, stemming, synonyms), not a general database. Every field is analyzed (tokenized, lowercased) unless explicitly marked as not analyzed (keyword fields).
- Inverted indexes (term → list of documents) make text search fast; you can't efficiently search by arbitrary numeric ranges or patterns without special indexes (B-tree for range, no free lunch).
- Shards distribute an index across nodes; replicas are copies of shards. A query hits all relevant shards in parallel; results are merged at the coordinating node. More shards = more parallelism but smaller shard size = slower per-shard search.
- Aggregations compute statistics (counts, sums, averages, distinct values) across matching documents. Bucket aggregations (group by field) and metric aggregations (compute stat per bucket) enable analytics without storing raw data separately.
- Writes are replicated asynchronously; a write is acknowledged to the client when it reaches the primary shard, but replicas lag. Read your own writes only on primary; replicas may return stale data.

## Apex practices
- Design mappings with analysis in mind: use text fields for full-text search (analysis enabled), keyword fields for exact match (no analysis), and numeric fields for ranges. Mapping changes require reindexing (copy data to new index).
- Set shard count based on data size and query load: 1-5GB per shard is typical. Too many shards = slow queries (fan-out overhead); too few = hotspots. Monitor shard sizes and rebalance as data grows.
- Use bulk API (/_bulk) for large inserts/updates, not one-at-a-time requests. Bulk reduces network overhead and enables parallelism.
- Enable refresh intervals appropriately: default 1s means 1s lag before indexed data is searchable. Increase to 30s+ for bulk loads (refresh after bulk completes). Too many refreshes = write amplification.

## Pitfalls
- Creating a new index per day (or per hour) with default 5 shards each; thousands of tiny shards cause slow queries and overhead. Use ILM (index lifecycle management) to roll over indices by size, not time.
- Storing all fields as text (analyzed) and then querying with exact match; use keyword fields for exact match to save space and speed up searches.
- Not setting mapping for dynamic fields; Elasticsearch infers types (often incorrectly), creating unexpected mappings when new fields arrive. Use strict mappings or dynamic: false to prevent surprises.

## Tools & references
Elasticsearch documentation (mapping, queries, aggregations), Kibana (visualization), "Elasticsearch: The Definitive Guide" (Clinton & Gormley), query DSL (bool, match, range, agg), field data vs doc values.
