# MySQL

## Scope
Relational database optimized for web applications. InnoDB engine (transactions, clustering), replication, and tuning for read-heavy workloads. MariaDB as a compatible fork.

## Core principles
- InnoDB is the standard storage engine since MySQL 5.5; it's transactional (ACID), uses clustered indexes (primary key IS the index), and supports foreign keys. MyISAM is legacy — don't use it for new projects.
- Clustered indexes mean the primary key determines row storage order on disk. Secondary indexes point to primary key, not row pointers. So every secondary index lookup requires a primary-key lookup (double the I/O). This favors small, low-cardinality primary keys (not 16-byte UUIDs).
- Row format (Compact vs Dynamic vs Compressed) affects storage and speed. Compressed rows save disk I/O and replication bandwidth but cost CPU. Profile before enabling compression on large tables.
- MySQL replication is async by default: the primary writes to binlog, slaves stream and apply the same writes. Lag is common in high-load scenarios. Semisynchronous replication waits for one slave's ACK before committing (slower but safer).
- Binlog (binary log) is required for replication and backup. Format: statement-based (SQL strings, smaller but non-deterministic for functions), row-based (exact row changes, large but safe), or mixed. Row-based is safer.

## Apex practices
- Set `innodb_buffer_pool_size` to 70–80% of available RAM; this is the cache for data and indexes. If the working set doesn't fit, performance degrades to disk I/O. Monitor `Innodb_buffer_pool_reads` (cache misses).
- Use `SHOW ENGINE INNODB STATUS` to diagnose lock waits and transaction state; if transactions are stuck, see which thread has the lock.
- Enable `slow_query_log` and `log_queries_not_using_indexes` to find problematic queries; use `pt-query-digest` (from Percona Toolkit) for analysis.
- Bulk load with `LOAD DATA INFILE` (faster than INSERT) and disable foreign-key checks temporarily. Re-enable after. This speeds up migrations.

## Pitfalls
- Using AUTO_INCREMENT for distributed IDs in a replication setup (ID collisions across shards); use UUIDs or sequence tables instead.
- Not setting `max_connections` and `max_allowed_packet` appropriately; the defaults are tiny and cause mysterious failures under load.
- Ignoring binlog format: statement-based replication with non-deterministic functions (NOW(), UUID(), RAND()) causes divergence between primary and replicas.

## Tools & references
MySQL documentation, Percona Toolkit (pt-query-digest, pt-duplicate-key-checker, pt-mysql-summary), "High Performance MySQL" (Schwartz, Zaitsev, Tkachenko), MySQL performance schema.
