# Self-Hosting

## Scope
Running infrastructure and applications on owned hardware or private clouds instead of managed services: operational burden, compliance, and cost trade-offs.

## Core principles
- Self-hosting trades operational complexity for cost and control — you own patching, backups, failover, scaling, and upgrades.
- Data gravity and latency are real reasons to self-host (regulatory residency, low-latency local services) — cost alone is rarely sufficient if you include ops labor.
- Self-hosting requires more automation (Kubernetes, configuration management) because you can't rely on managed service scaling and reliability — manual ops becomes unscalable.
- SLO ownership is now explicit — a managed database handles failover; a self-hosted database is your responsibility (recovery time objective, recovery point objective).
- Security model changes — you manage the full stack (kernel patches, networking, access control), which is more surface area but finer-grained control.

## Apex practices
- Automate everything (infrastructure provisioning, backup, recovery, updates) or self-hosting will fail — manual ops scales linearly with machines, automation scales logarithmically.
- Implement comprehensive monitoring (hardware health, capacity, performance) — discovering a failing disk during an outage is worse than discovering it proactively.
- Test your disaster recovery (backups, failover, recovery procedures) at least quarterly — untested backups are not backups.
- Ensure compliance is actually achievable — self-hosting is only worth it if the regulatory or operational benefits outweigh the costs; document trade-offs.

## Pitfalls
- Underestimating operational overhead (hardware procurement, maintenance, version upgrades) — it's not just about saving on cloud bills.
- Self-hosting without proper monitoring and alerting (you don't know about problems until customers report them).
- No plan for capacity or upgrades (running at 90% capacity, no growth headroom) — self-hosted infrastructure needs buffer.

## Tools & references
Kubernetes on bare metal (Kubeadm, Kubespray), cluster administrators' guild, UpCloud, Hetzner, Equinix Metal, infrastructure automation (Ansible, Terraform).
