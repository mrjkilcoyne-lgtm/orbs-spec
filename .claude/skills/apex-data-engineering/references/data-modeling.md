# Data Modeling

## Scope
Structuring analytical data: dimensional modeling (star/snowflake), Data Vault, wide tables, and choosing grain, keys, and slowly changing dimension strategy.

## Core principles
- Declare the grain first — "one row per order line per day" — before choosing any dimension or fact; every downstream bug traces back to an ambiguous or drifting grain.
- Kimball star schemas optimize for query comprehension and BI-tool joins; Data Vault (hubs/links/satellites) optimizes for auditability and parallel loading; Inmon 3NF optimizes for integration — pick per layer, not per religion.
- Facts are numeric and additive (or explicitly semi-/non-additive like account balances and ratios); dimensions are the descriptive context you filter and group by. Mixing them creates un-aggregatable tables.
- Slowly Changing Dimensions are a contract: Type 1 overwrites (loses history), Type 2 versions rows with effective/expiry dates and a current flag (the default for anything auditors touch), Type 3 keeps a prior-value column. Choose per attribute, not per table.
- Surrogate keys decouple your model from source-system key churn and enable Type 2 history; natural keys still belong in the table as durable business identifiers for lineage and dedup.

## Apex practices
- Build a conformed-dimension bus matrix (processes × dimensions) before writing DDL — shared `dim_customer` and `dim_date` are what make cross-process analysis possible.
- Model many-to-many and multi-valued attributes with bridge tables carrying allocation weights, rather than exploding fact grain or comma-packing values.
- In columnar cloud warehouses, denormalize snowflakes into flat dimensions and consider "one big table" for hot dashboards — storage is cheap, joins at query time are not free — but keep the star as the governed source.
- Use degenerate dimensions (order number lives on the fact) and junk dimensions (bundle low-cardinality flags into one small dim) to keep fact tables narrow and dimension counts sane.

## Pitfalls
- Fan-out from joining a fact to a dimension at the wrong grain, silently double-counting revenue — the classic "numbers went up after the join" bug.
- Type 2 SCDs without a reliable change-detection mechanism (hash-diff or CDC), producing either missed history or a new version every load.
- Modeling straight from source-system schemas ("just copy the OLTP tables") so every report re-implements business logic in its own WHERE clauses.

## Tools & references
Kimball & Ross "The Data Warehouse Toolkit" (3rd ed.), Linstedt's Data Vault 2.0, dbt dimensional modeling guides, "Agile Data Warehouse Design" (Corr & Stagnitto).
