# Autoscaling

## Scope
Dynamically adjusting compute resources (pods, nodes, instances) based on demand with predictability and cost efficiency.

## Core principles
- Horizontal scaling (more instances) is always better than vertical (bigger instances) — you avoid single points of failure and can scale to arbitrary load.
- Autoscaling metrics matter: request rate scales linearly, CPU usage is unreliable (workload-dependent), custom metrics (queue depth, business metrics) are best.
- Autoscaling has lag (detection delay + provisioning delay); overshoot (scaling too far up) wastes money, undershoot (scaling too little) causes thrashing.
- Scaling down is harder than scaling up — you must ensure you don't evict in-flight requests (connection draining, pod disruption budgets) or lose data.
- Autoscaling at multiple levels (pod autoscaler + node autoscaler) can interact badly — a scale-down event on nodes kills freshly-scaled pods, defeating the purpose.

## Apex practices
- Use Horizontal Pod Autoscaler (HPA) on metrics that predict load, not after the fact — request count or custom metrics; set CPU limits correctly (requests at P50, limits at P95).
- Configure target utilization conservatively (60-70% for safety); if you target 90% utilization, normal variance causes thrashing.
- Set min/max pod replicas to avoid oscillation (if max is 2 and load bounces between 1 and 2 pods, you get constant churn).
- Use Karpenter or Cluster Autoscaler for node scaling, not just pod scaling — ensure nodes exist for the pods that HPA spins up, test scale-down scenarios.

## Pitfalls
- Autoscaling on CPU usage (too noisy, responds to spikes after they happen) — use request count or custom metrics instead.
- No minimum replicas in production (crash of a single instance causes cascading failures while autoscaler is provisioning) — always run at least 2.
- Autoscaling without drain time (connections are severed mid-request) — implement graceful shutdown and connection draining.

## Tools & references
Kubernetes HPA, KEDA for custom metrics, Karpenter for node autoscaling, Cluster Autoscaler, Prometheus for metrics, pod disruption budgets.
