# Data Egress & Bandwidth

## Scope
Understanding and minimizing data transfer costs between cloud services, regions, and the internet.

## Core principles
- Data egress (moving data out) is expensive; data ingress (moving in) is usually free; this asymmetry affects architecture.
- Cross-region replication incurs egress charges on the origin and ingress charges on the destination; it's not a secret cost.
- Internet egress is the most expensive; egress to CDN is cheaper; egress within a region (to other services) is free or cheap.
- Data transfer between services in the same availability zone (AZ) is free on AWS; cross-AZ is charged; cross-region is expensive.
- High-bandwidth workloads (streaming video, large file downloads) can bankrupt you if not planned; charge customers or sponsor via sponsored egress.

## Apex practices
- Use AWS VPC endpoints for S3 and DynamoDB to avoid egress charges; traffic stays within AWS network.
- Use CloudFront (AWS CDN) for content distribution; CDN egress is cheaper than direct internet egress.
- Keep databases and compute in the same region or AZ; cross-AZ queries incur egress charges.
- Monitor egress (many cloud providers expose it as a metric in billing); set alerts on anomalies (unexpected large data transfers).

## Pitfalls
- Assuming replication is cheap; cross-region replication can cost more than storage.
- Streaming large datasets to the internet without a CDN — enable CDN from day one.
- No visibility into egress costs; they're often the second-largest bill after compute (after storage).

## Tools & references
AWS Cost Explorer (filter by data transfer), CloudFront pricing, Cross-region replication costs, VPC endpoint pricing, CDN providers (Cloudflare, Fastly, Bunny).
