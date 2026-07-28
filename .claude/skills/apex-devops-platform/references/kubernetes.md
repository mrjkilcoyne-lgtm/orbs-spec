# Kubernetes

## Scope
Orchestrating containerized workloads at scale: cluster architecture, pod lifecycle, networking, storage, and resource management.

## Core principles
- Kubernetes abstracts infrastructure but does not hide it — resource requests/limits, node affinity, and drain behavior must be explicit or you'll hit cascade failures.
- Pods are the unit of orchestration, not containers; sidecar and init patterns unlock most of Kubernetes' power, but tight coupling is the risk.
- StatelessPods are designed for cattle, not pets — if you're stateful, use StatefulSets with persistent volumes and accept the complexity; half-measures lead to silent data loss.
- NetworkPolicies default-allow, which means you must explicitly deny or isolate; "security by namespace" is not security.
- etcd is the source of truth for cluster state; its consistency is non-negotiable — a split-brain etcd cluster is worse than a crashed one.

## Apex practices
- Set requests/limits correctly: requests drive scheduling (pods won't land without capacity), limits prevent noisy neighbors — set requests to 80% of peak usage in QA, then adjust up if you're getting evictions.
- Use horizontal pod autoscaling (HPA) on metrics that actually predict load — request count, not CPU usage (CPU lags; use custom metrics instead).
- Adopt a service mesh (Istio, Linkerd) only after solving basic networking — ingress routing, mTLS, circuit breaking — first with sidecar-free approaches; a mesh scales troubleshooting surface area.
- Run pod security policies and pod security standards; audit what's actually running (Falco, Cilium runtime enforcement) to catch both misconfig and lateral movement.

## Pitfalls
- Setting no resource requests/limits and calling it flexibility — it's chaos; the cluster falls over unpredictably.
- Using Kubernetes for stateful databases with dynamic provisioning (you will lose data on a node failure during a resize).
- Configuring cluster autoscaling without a clear node utilization policy — runaway costs and inefficient packing are the norm.

## Tools & references
Kubernetes docs (official), "Kubernetes the Hard Way", CNCF Kubernetes maturity matrix, kube-bench for compliance, Falco for runtime security.
