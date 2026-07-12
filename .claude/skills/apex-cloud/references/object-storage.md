# Object Storage

## Scope
Scalable, durable storage for unstructured data: S3, GCS, Azure Blob Storage, and lifecycle management.

## Core principles
- Object storage is write-once-read-many; updates are atomic but not in-place (a new object version is created).
- Durability (data never lost) comes from replication; multi-region replication is explicit and costs money (egress charges).
- Access patterns should be visible in bucket design (versioning, lifecycle policies, access logs); random access to thousands of small files is inefficient.
- Cost is driven by storage, requests, and egress — monitor all three; egress charges across regions or to the internet are often the largest cost.
- Object metadata (tags, ACLs, headers) can be queried but not indexed efficiently; for queryable metadata, use a database.

## Apex practices
- Use lifecycle policies to move old data to cold storage (Glacier, Archive) automatically; cold storage is 90% cheaper than hot storage.
- Enable versioning and implement retention policies (Object Lock) for regulatory compliance; you can't accidentally delete if retention is enforced.
- Use multi-region replication for critical data but understand the cost and consistency model (eventual consistency, not immediate).
- Implement S3 inventory for large buckets (billions of objects) to get metadata without listing all objects (too slow).

## Pitfalls
- Storing frequently-accessed data in cold storage (retrieval is slow and expensive) — use hot storage for hot data, move cold data after TTL.
- No retention/deletion policy (buckets grow unbounded, storage costs explode) — implement retention at creation time.
- Versioning without cleanup (old versions accumulate) — use lifecycle rules to delete old versions after retention period.

## Tools & references
AWS S3, GCP Cloud Storage, Azure Blob Storage, Terraform, S3 Select for querying without loading all data, Wasabi for S3-compatible alternative.
