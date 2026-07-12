# Schema Evolution

## Scope
Changing data schemas without breaking producers, consumers, or history: compatibility modes, evolution rules per format, and managing change across pipeline boundaries.

## Core principles
- Compatibility is directional and you must pick one: backward (new readers read old data — consumers upgrade first... actually: new schema reads old data, so upgrade consumers freely), forward (old readers read new data — producers can move first), or full (both). Schema Registry enforces the declared mode per subject; choosing "none" is choosing outages.
- The universally safe moves are few: add an optional/defaulted field, widen a type (int→long), relax a constraint. Renames, type narrowing, semantic redefinition ("amount is now in cents"), and required-field additions are breaking — and the semantic ones are the worst because nothing detects them.
- Every format has different rules: Avro resolves by field name with defaults required for evolution; Protobuf resolves by field number (never reuse or renumber; `reserved` retired numbers); Parquet/Iceberg track columns by field ID so renames are metadata-only; JSON has no rules, only hope and validation.
- Schemas are contracts between teams, not internal implementation details: evolution must be governed at the boundary (registry compatibility checks in CI, data contracts, deprecation windows) because the producer who "just added a column" cannot see the consumer whose MERGE now fails.
- History constrains you forever: old data written with old schemas remains readable only if evolution rules were followed from day one — a lake with five incompatible generations of the "same" table is an archaeology project, not a dataset.

## Apex practices
- Put schema-compatibility checks in producer CI (registry check, buf breaking for Protobuf, Iceberg schema diff) so breaking changes fail the build, not the 2am pipeline run.
- Execute renames as expand-and-contract: add new column, dual-write, backfill, migrate consumers with a deadline, then drop — never in-place rename across a producer/consumer boundary (except in field-ID formats like Iceberg where it's genuinely safe).
- Version semantics explicitly when meaning changes: a new field name (`amount_cents`) or a schema/topic version bump — reusing a field with new meaning is the one change no tooling can catch.
- Keep the raw layer schema-permissive (land unexpected fields into a variant/JSON column rather than dropping them) and enforce strictness at the staging layer, so upstream surprises are captured, visible, and non-fatal.

## Pitfalls
- Protobuf field-number reuse after deleting a field — old data decodes into the new field as garbage, silently.
- Hive-style Parquet tables resolving columns by position: dropping a middle column shifts every subsequent column's data into the wrong name.
- Adding a NOT NULL/required field with no default and breaking every reader of historical records that lack it.

## Tools & references
Confluent Schema Registry compatibility docs, Avro spec (schema resolution), Protobuf language guide (field numbers, reserved), Iceberg schema evolution docs, buf breaking-change detection, Kleppmann's DDIA ch. 4.
