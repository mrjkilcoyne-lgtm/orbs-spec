# Columnar Formats (Parquet / ORC / Arrow)

## Scope
On-disk and in-memory columnar data layouts: Parquet and ORC file internals, Arrow as the in-memory interchange standard, and how encoding choices drive scan performance.

## Core principles
- Columnar layout wins for analytics because queries touch few columns and many rows: reading only needed columns plus per-column compression (similar values compress better) typically cuts I/O 10-100x versus row formats.
- Parquet's hierarchy matters: file → row groups (~128MB-1GB, the unit of parallelism) → column chunks → pages (the unit of encoding/compression). Row-group min/max statistics enable predicate pushdown that skips whole groups without reading them.
- Encodings do the heavy lifting before compression: dictionary encoding for low-cardinality columns, run-length encoding for repeated values, delta encoding for sorted numerics — a sorted low-cardinality column can be 100x smaller than the same data shuffled.
- Arrow is not a file format; it's a zero-copy in-memory columnar specification so engines (pandas, DuckDB, Spark, Polars, DataFusion) can hand off data without serialization — Arrow Flight extends this over the network, and ADBC over database connections.
- Nested data in Parquet uses Dremel-style definition/repetition levels (from Google's Dremel paper), which is why deeply nested schemas carry real encoding overhead and shredding structs into columns still allows selective reads.

## Apex practices
- Sort data within files on the dominant filter column before writing: it maximizes RLE/dictionary efficiency and makes min/max pruning surgical instead of useless.
- Choose compression per workload: ZSTD for best ratio at good speed (the modern default), Snappy for CPU-bound scan speed; benchmark on your data, and never gzip Parquet you plan to scan hot.
- Keep files 128MB-1GB and row groups aligned with them; verify pushdown actually happens with the engine's scan stats (rows read vs rows returned), not by assumption.
- Watch types at boundaries: Parquet timestamp units (millis/micros/nanos), INT96 legacy timestamps, and decimal precision are the classic cross-engine corruption points — pin schemas explicitly rather than trusting inference.

## Pitfalls
- Writing Parquet with one row group per row (or thousands of tiny files) via naive streaming writers, destroying both compression and pruning.
- High-cardinality strings (UUIDs) as dictionary-encoded columns — dictionaries overflow, pages balloon; consider byte-array plain encoding or restructure keys.
- Assuming CSV→Parquet conversion preserves semantics: nulls vs empty strings, type inference on the first N rows, and float precision all silently change data.

## Tools & references
Apache Parquet format spec, Apache Arrow docs (and the ADBC/Flight subprojects), Google's Dremel paper (VLDB 2010), ORC spec, parquet-tools/pyarrow for inspection.
