# Feature Stores

## Scope
Centralized storage and serving of ML features: point-in-time correctness, online/offline consistency, feature versioning, and reducing training-serving skew.

## Core principles
- Point-in-time correctness is non-negotiable: at prediction time, your model must see the exact feature values it saw during training (same aggregation window, same business-logic version). Serve from a feature store with immutable snapshots or deterministic replay.
- Online/offline split is the architecture: offline store (warehouse) for training datasets (feature histories with serving-time labels), online store (cache/DB) for sub-millisecond feature serving in production. Both must read from the same source-of-truth feature definitions.
- Feature versioning prevents silent breakage: production models depend on specific feature schemas and transformations. Versioned feature definitions, backwards-compatible schema evolution, and canary deploys make feature updates safe.
- Recomputation and backfill must be deterministic: same feature code on the same input timestamp must produce the same output. Non-determinism (UUIDs in feature logic, wall-clock dependencies, floating-point precision) breaks the contract between training and serving.
- Latency tier spans 10^7: batch features (1–24h old acceptable, microsecond compute at query time), streaming features (seconds old, precalculated), and request-time features (sub-100ms, computed on the fly). Layer them explicitly — never compute hour-old features at request time.

## Apex practices
- Build feature definitions as code (Feast, Tecton, or in-house SQL): declarative schema, transformation logic, and serving tier in one place. Auto-generate the offline (warehouse view + training export) and online (Redis/DynamoDB schema + loader) surfaces.
- Track lineage: which raw tables feed which features, which features feed which models. Materialization DAGs (batch or streaming) are your dependency graph and backfill orchestration.
- Implement feature-level monitoring: schema validity, nullability rates, distribution drift (mean/percentiles), and redundancy checks (e.g., feature_x is always 1.5 * feature_y). Catch data breakage before models surprise you in production.
- Replay features at serving time when latency allows: compute request-time features fresh using the same aggregation and business logic as training, not cached stale versions. Replay cost often beats the precision loss from staleness.

## Pitfalls
- Training set built from the current feature store (no snapshot), then production model served from yesterday's cached values — label leakage and serving skew in one architectural flaw.
- Non-deterministic feature logic (RAND(), NOW(), row_number() without ORDER BY) that produces different values across training and serving runs.
- Orphaned features: no one owns versioning or backfill, so old code breaks when the upstream table schema changes or is deleted.

## Tools & references
Feast, Tecton, Hopsworks, "Designing Machine Learning Systems" (Huyen), MLflow for feature tracking, point-in-time joins (SQL window functions with effective dates).
