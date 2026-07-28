# Data Governance

## Scope
Making data trustworthy, discoverable, and compliant at organizational scale: ownership, catalogs, access control, PII handling, retention, and regulatory obligations (GDPR/CCPA).

## Core principles
- Governance without named owners is theater: every dataset needs an accountable owner (a team, not a person who might leave) with defined duties — respond to quality incidents, approve access, steward the schema. The org chart is the hardest part of governance, not the tooling.
- Classify data by sensitivity (public / internal / confidential / PII / regulated) at the column level, and let classification drive mechanical policy: masking, access tiers, retention, allowed destinations. Unclassified data defaults to restricted, or classification never happens.
- Regulatory requirements are architectural: GDPR's right to erasure means you must be able to find and delete one person's data everywhere — which forces keyed deletes in lakes (why Iceberg/Delta deletes matter), crypto-shredding for immutable stores, and lineage to know "everywhere."
- Least-privilege access scales only through automation: role/attribute-based access mapped to groups, self-service requests with owner approval and expiry, and periodic access recertification — hand-granted permanent grants accrete into everyone-can-read-everything within two years.
- Governance earns adoption by accelerating, not gatekeeping: a catalog that makes trusted data findable in minutes gets used; a review board adding three weeks to every schema change gets routed around — and shadow data is ungoverned data.

## Apex practices
- Deploy an automated catalog (DataHub, Collibra, Unity/Purview) fed by pipelines — schema, lineage, ownership, freshness, classification harvested automatically — with humans adding only descriptions and business context.
- Automate PII discovery (pattern + ML scanners over columns) and apply policy at the platform layer: dynamic masking, tokenization for analytics on sensitive fields, purpose-scoped access for regulated uses.
- Encode retention as executable policy per classification (table TTLs, partition expiry, archive tiers) with deletion evidence logged — "we keep everything forever" is both a compliance violation and a liability under discovery.
- Certify golden datasets: a visible tier ("certified" badge, guaranteed SLA, tested definitions) that consumers prefer by default — governance through a pit of success rather than through prohibition.

## Pitfalls
- Governance-by-committee producing policy documents but no enforcement mechanism — if policy isn't executed by platform code, it's a wish.
- Copying production PII into dev/test/sandbox environments where controls don't follow — most leaks come from the ungoverned copy, not the governed original.
- Ignoring the deletion path until the first GDPR erasure request arrives against 5 years of immutable Parquet with no per-subject keys.

## Tools & references
DAMA-DMBOK, DataHub/Collibra/Alation/Unity Catalog/Purview, GDPR Art. 17 and CCPA texts, crypto-shredding pattern, "Data Mesh" (Dehghani) on federated computational governance.
