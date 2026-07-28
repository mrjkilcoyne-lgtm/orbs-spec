# SQLite

## Scope
Serverless, file-based SQL database for embedded and mobile use. ACIDity, minimal configuration, excellent for low-concurrency workloads and offline-first apps.

## Core principles
- SQLite has one writer at a time (the entire database is locked during WRITE); readers can run concurrently with reads, but a writer blocks everything. This is fine for low-contention access (single app, few concurrent users) but breaks under concurrent writes (multiple processes competing for the lock).
- WAL mode (Write-Ahead Logging) decouples readers and writers: writes go to a journal first, then are checkpointed to the main DB asynchronously. Readers can see the main DB while writes accumulate in the journal. Much better concurrency than the default rollback journal.
- SQLite is fully ACID and supports transactions; `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK` work correctly. Durability depends on filesystem calls (fsync), so honor `PRAGMA synchronous` tradeoffs (FULL is safe, NORMAL is faster, OFF is risky).
- No network overhead: SQLite is linked into your process. Queries are absurdly fast (1M inserts per second on modern hardware with fsync disabled). Ideal for offline-first (local cache), embedded systems, and test databases.
- Weak typing: SQLite accepts any type in any column (you can store text in an integer column). Constraints exist (CHECK, NOT NULL, UNIQUE) but aren't enforced as strictly as in PostgreSQL or MySQL.

## Apex practices
- Enable WAL mode and PRAGMA optimize for production: `PRAGMA journal_mode = WAL; PRAGMA optimize;`. This unlocks concurrency and updates statistics.
- Use connection pooling even with SQLite (via libraries like sqlalchemy for Python) to avoid repeated open/close overhead. Connections in WAL mode are cheap.
- Set `PRAGMA foreign_keys = ON` to enforce referential integrity; it's off by default for legacy compatibility.
- For larger datasets or high-concurrency needs, SQLite reaches limits (tens of GB, high write contention). Plan migration to PostgreSQL/MySQL if you outgrow it.

## Pitfalls
- Treating SQLite as a toy database; it's production-ready for its use case (embedded, mobile, offline-first, testing) but not for high-concurrency server workloads.
- Disabling fsync (PRAGMA synchronous = OFF) for speed without understanding data loss risk; the database can corrupt silently if the OS crashes during a write.
- Using SQLite's lax type system without constraints; relying on application logic to enforce types is fragile.

## Tools & references
SQLite documentation (pragma, WAL mode, recovery), Datasette (web UI for SQLite exploration), "SQLite the Definitive Guide" (Owens & Allen), sqlalchemy for Python, D.Richard Hipp's talks on design philosophy.
