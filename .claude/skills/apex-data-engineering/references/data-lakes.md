# Data Lakes

## Scope
Object-storage-based data platforms: lake layout, open table formats (Delta Lake, Iceberg, Hudi), lakehouse architecture, and avoiding the data swamp.

## Core principles
- A lake is object storage plus discipline: without enforced layout, ownership, schemas, and a catalog, it degrades into a data swamp — the discipline is the product, S3 is just the substrate.
- Open table formats (Iceberg, Delta, Hudi) turn files into tables: ACID commits via a metadata/manifest layer, snapshot isolation, schema evolution, time travel, and safe concurrent writers — raw Parquet-in-directories gives you none of that.
- The medallion pattern (bronze = raw immutable, silver = cleaned/conformed, gold = business aggregates) is about re-derivability: any downstream layer can be rebuilt from bronze, so bronze is append-only and never "fixed" in place.
- Object stores are not filesystems: list operations are slow and eventually cost-dominant, renames are copies, and small files are poison — target 128MB–1GB files and compact continuously.
- The catalog is the control plane: Iceberg/Delta tables are only as consistent as the catalog (Glue, Hive Metastore, Unity, Nessie, REST catalog) that arbitrates commits — choose it as carefully as you'd choose a database.

## Apex practices
- Default to Iceberg or Delta for anything queried by more than one engine; check writer/reader support matrix per engine (Spark, Trino, Flink, Snowflake, DuckDB) before committing to format features like merge-on-read.
- Schedule table maintenance as a first-class pipeline: small-file compaction, snapshot expiration, orphan-file cleanup, and manifest rewrite — unmaintained Iceberg/Delta tables slow down and cost more every week.
- Partition by low-cardinality columns aligned to query filters (dates, regions), use Iceberg hidden partitioning to decouple layout from queries, and rely on file-level column stats for finer pruning.
- Encode access control at the table/catalog layer (Lake Formation, Unity Catalog, Ranger), not via bucket ACL archaeology; bucket-level policies cannot express column or row rules.

## Pitfalls
- The small-files problem: streaming or per-event writes producing millions of KB-sized files, making listing and query planning slower than the actual scan.
- "Schema on read" used as an excuse to skip contracts, so every consumer parses the same raw JSON differently and gets different answers.
- Time travel and snapshots retained forever "just in case," tripling storage cost and slowing metadata operations — set retention policies deliberately.

## Tools & references
Apache Iceberg spec and docs, Delta Lake (Databricks "Lakehouse" paper, CIDR 2021), Apache Hudi, AWS Lake Formation / Unity Catalog / Project Nessie, Trino and Spark as query engines.
