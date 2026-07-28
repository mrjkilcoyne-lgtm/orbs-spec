# Hybrid Cloud

## Scope
Integrating on-premises infrastructure with cloud services: connectivity, data consistency, and operational complexity.

## Core principles
- Hybrid cloud is not a default; it adds complexity (networking, data sync, operational tooling) — use it when you have a genuine constraint (regulation, legacy systems, cost).
- Network latency between on-prem and cloud (tens of milliseconds) affects application design — chatty APIs fail; batch and async are required.
- Data consistency across hybrid systems requires planning: sync-first (data starts on-prem), cloud-first (data starts in cloud), or dual-write (complex, hard to keep in sync).
- Operational tooling must span both (monitoring, logging, provisioning); fragmented tools create blind spots and slow incident response.
- Security boundaries require hardening: dedicated network connections (Direct Connect, ExpressRoute, Interconnect), encryption in transit, strict access control.

## Apex practices
- Use dedicated network connections (not internet) between on-prem and cloud for security and performance.
- Implement data synchronization with clear direction (on-prem → cloud or cloud → on-prem, not bidirectional) and conflict resolution.
- Treat on-prem and cloud as separate regions in your disaster recovery plan; test failover from one to the other.
- Use containers and Kubernetes to abstract underlying infrastructure; reduce operational differences between on-prem and cloud.

## Pitfalls
- Assuming hybrid cloud is cheaper (it's usually more expensive operationally) — do a TCO analysis.
- No plan for networking latency (synchronous calls across WAN fail) — design for asynchronous, batched updates.
- Data replication without conflict resolution (bidirectional sync fails when conflicts occur) — pick a source of truth.

## Tools & references
AWS Direct Connect, GCP Dedicated Interconnect, Azure ExpressRoute, Kubernetes on-prem, data replication tools (DMS, BigQuery Transfer Service), networking best practices.
