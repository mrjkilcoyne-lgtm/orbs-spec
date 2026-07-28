# Relational Design

## Scope
Structuring tables, columns, and constraints to model domain logic and enable efficient queries. Table design, cardinality, uniqueness, and referential integrity.

## Core principles
- Declare the natural key first (unique identifier from the domain, e.g., ISBN for books), then add a surrogate primary key if needed for manageability and foreign-key linking. Natural keys are contracts — preserve them as unique constraints even if you use surrogate PKs.
- Denormalization is an optimization, not a default: start normalized (every fact in one place) so business-logic changes don't cascade. Denormalize deliberately (cache a computed column, duplicate an attribute for performance) with a maintenance story.
- Cardinality at table design time drives indexing, partitioning, and query strategy: millions of rows query differently than billions. Anticipate growth — "this table is mostly analytical" vs "this is OLTP" determines whether you sort by insertion order or cluster on user_id.
- Constraints encode domain rules: NOT NULL means "this exists," UNIQUE means "no duplicates," CHECK means "this value is valid." Let the DB enforce them rather than hoping application code remembers.
- Entity-Attribute-Value (EAV) and JSON-in-relational trades schema flexibility for query complexity; use them for truly unstructured data (user metadata), not to avoid schema design. A schemaless table is just a table with every column nullable-text and a parser in your app.

## Apex practices
- Use explicit enum types (PostgreSQL ENUM, MySQL check constraints) rather than string columns with implicit rules. The DB catches typos; your application doesn't.
- Model many-to-many with an explicit junction table (user_id, role_id, effective_date) rather than packing IDs into an array or JSON. This is the classic second-normal-form pattern and keeps queries joinable.
- Keep highly-normalized tables normalized at write-time; materialize denormalized views (or ETL-derived tables) for read-heavy patterns. This separates the write model (precise) from the read model (fast).
- Design every table with an immutable, queryable created_at timestamp and updatable updated_at. Track changes with an audit table or CDC, not by hoping you can infer edits from stale data.

## Pitfalls
- Chasing the normalization ideal beyond 3NF, creating dozens of tiny join-heavy tables that are slower than a well-indexed denormalized one.
- Modeling everything as polymorphic ("types" column + EAV) instead of separate tables for different entity kinds, making queries slow and correctness unclear.
- Forgetting NULL semantics: NULL is "unknown," not "empty" or zero. Filters and aggregations behave differently, and the DB won't enforce constraints on NULL values.

## Tools & references
"Database Design Manual" (Lightstone, Teorey, Nadeau), C.J. Date's relational algebra and "An Introduction to Database Systems," normalization forms (1NF–BCNF), PostgreSQL/MySQL schema documentation.
