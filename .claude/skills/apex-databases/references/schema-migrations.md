# Schema Migrations

## Scope
Evolving database schemas over time: adding/removing columns, changing types, and maintaining backwards compatibility. Online migrations without downtime.

## Core principles
- Schema changes must be backwards compatible: the new schema works with old application code (during deployment), and the old schema works with new code (during rollback). Violating this breaks deployments.
- DDL (Data Definition Language) operations lock tables in traditional databases: ALTER TABLE ADD COLUMN blocks writes until complete. Large tables = long locks = downtime. Modern databases (PostgreSQL 11+, MySQL 8.0+) support online DDL with minimal locking.
- Coordinate with application deployments: rolling deployments assume both old and new code coexist. If the new code expects a column that doesn't exist yet, it crashes. Deploy schema first, then application (or use feature flags to activate new code after column exists).
- Reversibility: every migration needs an "undo" (rollback) script. A migration that removes data (DROP COLUMN without dumping to archive) is irreversible; if rollback is required, data is lost.
- Large data changes (backfilling millions of rows) should be batched: UPDATE 10K rows, commit, repeat. Holds locks for less time, doesn't exhaust memory, and can be paused if needed.

## Apex practices
- Use a migration framework (Flyway, Liquibase, Alembic for Python, Rails migrations) to version schemas and apply migrations in order. Never apply DDL manually (error-prone, unversioned).
- Test migrations on production-sized data (or a snapshot) before applying to production. A migration fast on a test table (1K rows) might take hours on 1B rows.
- Always backfill data in the application, not in the migration script: deploy code that fills the new column as writes happen, run a backfill job for existing data. Decouples schema from data changes.
- Implement feature flags in the application: deploy code that handles both old and new schema, then apply the migration, then remove the feature flag (or vice versa for rollback). Provides safe reversibility.

## Pitfalls
- Not planning for reversal: a migration that renames a column, then the application crashes on the new name — rollback fails because the old name is gone.
- Migrating schema and data in one massive transaction; if the migration fails halfway (usually due to locks or running out of memory), rollback is slow. Break into smaller transactions.
- Assuming zero downtime without understanding locking: online DDL (PostgreSQL CONCURRENTLY, MySQL ALGORITHM=INPLACE) is available but has constraints (no foreign keys, no indexes to add simultaneously). Test thoroughly.

## Tools & references
Flyway, Liquibase, Alembic, Rails migrations, "Zero Downtime Deployments" (Beyer), pg_surgery (PostgreSQL offline repair), gh-ost (online table migration for MySQL), backward-compatibility verification tools.
