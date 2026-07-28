# DR Testing

## Scope
Disaster recovery drills: testing failover procedures, validating backup recovery, and ensuring runbooks are current.

## Core principles
- Recovery time objective (RTO) is the acceptable downtime; recovery point objective (RPO) is the acceptable data loss.
- A untested disaster plan is not a plan; failover procedures that have never been executed will fail when needed most.
- Failovers expose configuration issues (stale DNS, hardcoded IPs, missing credentials in the backup region).
- Data backup is only useful if it's been restored and validated; backups that can't be read are not backups.
- Regular DR drills (quarterly or semi-annual) keep procedures fresh and catch degradation (slower backup restore, new data types not backed up).

## Apex practices
- Schedule DR drills in advance; during drills, don't do real work, test the failover in a way that doesn't affect production.
- Document the RTO and RPO; design for them (if RTO is 1 hour, failover must complete in < 1 hour).
- Use chaos engineering (Gremlin, Chaos Mesh) to inject failures (kill instances, partition network) and verify recovery.
- Automate failover where possible (DNS flip, load balancer reconfiguration) to meet tight RTOs.

## Pitfalls
- DR plans that are not automated; manual failover is slow and error-prone, especially during high stress.
- Backups that are stored in the same region as production; a regional outage loses both.
- Not testing backup restore; a backup that can't be read when needed is worse than useless (false confidence).

## Tools & references
Chaos engineering (Gremlin, Chaos Mesh, Chaos Toolkit), backup validation (Veeam, Commvault), infrastructure-as-code (Terraform, CloudFormation) for reproducible failovers, multi-region deployment patterns (Terraform, Kubernetes).
