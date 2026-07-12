# Normalization

## Scope
Eliminating data redundancy through normal forms (1NF, 2NF, 3NF, BCNF). Identifying and resolving anomalies: insertion, update, deletion.

## Core principles
- Normalization removes redundancy so a single edit updates one place: in a non-normalized table with repeated (author, book) pairs, changing an author's name requires updating many rows. Normalized form has author data in one table, referenced by ID.
- First Normal Form (1NF): every column contains atomic (non-repeating) values. No arrays, JSON, or comma-separated lists. This is the baseline; violated 1NF breaks indexing, comparison, and aggregation.
- Second Normal Form (2NF): all non-key attributes depend on the entire key, not just part of it. If your table's key is (order_id, line_item_id) but product_name depends only on line_item_id, extract it: breaks the rule.
- Third Normal Form (3NF): non-key attributes don't depend on other non-key attributes. If salary_grade_id determines salary_range, store salary_grade_id, not the redundant range. Boyce-Codd Normal Form (BCNF) is stricter and more rarely necessary.
- Normalization costs reads (more joins), not writes (fewer updates per change). The tradeoff is declarative: normalized for write-heavy transactional systems, denormalized views for read-heavy analytical ones.

## Apex practices
- Test normalization by asking: "If I change this one fact, does it require updating one row or many?" If many, extract to a separate table and reference by ID.
- Use dependency diagrams to visualize functional dependencies (which attributes depend on which key components). Clarifies whether you're in 2NF or 3NF.
- Denormalize (cache a computed column or duplicate a foreign-key attribute) only when profiling shows the join is the bottleneck, and document the maintenance responsibility (trigger, ETL, or manual update).
- Stop at 3NF in practice; going to BCNF or 4NF usually doesn't pay for the complexity. Some redundancy is acceptable if the access pattern justifies it.

## Pitfalls
- Over-normalizing into a snowflake with dozens of single-column tables joined together, making queries unreadable and slow.
- Normalizing then forgetting to add indexes on foreign keys, so the normalized schema is slower than the original denormalized blob.
- Believing that normalization is always right; some workloads (data warehouses, document databases) are intentionally denormalized because reads vastly outnumber updates.

## Tools & references
C.J. Date "An Introduction to Database Systems" (normal forms chapter), "Database Design Manual" (Lightstone, Teorey), Codd's original papers on relational algebra.
