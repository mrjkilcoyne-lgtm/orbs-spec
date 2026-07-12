# Container Services

## Scope
Managed container orchestration: ECS, GKE, AKS; trade-offs between managed and self-hosted Kubernetes.

## Core principles
- Container services automate scaling, scheduling, and networking but the cost is complexity — use if you have 10+ services, not for one app.
- Kubernetes (GKE, EKS) is the most portable but also the most complex — consider managed Kubernetes only if you need it.
- Fargate (AWS) and Cloud Run abstract Kubernetes but constrain customization — good for simple workloads, limiting for stateful apps.
- Resource reservations (CPU, memory) drive scheduling decisions — over-provisioning wastes money, under-provisioning causes thrashing.
- Networking (service discovery, load balancing) is handled by the platform — configuration is required for multi-region or multi-cloud.

## Apex practices
- Use Fargate for simple stateless services (no instance management overhead); use ECS/EKS for complex workloads needing control.
- Implement health checks (liveness, readiness) so the platform can restart unhealthy containers and route traffic only to healthy ones.
- Use managed registries (ECR, Artifact Registry) integrated with the container service for automatic image pulls and vulnerability scanning.
- Implement resource limits (CPU, memory) per container and per deployment; auto-scaling needs these to make scaling decisions.

## Pitfalls
- Treating containers as VMs (long-running services with local state) — containers should be ephemeral and stateless.
- No health checks (bad containers never restart) — implement liveness and readiness probes.
- Single-instance services (no redundancy, crashes cause downtime) — always run at least 2 replicas.

## Tools & references
AWS ECS, EKS, GKE, AKS, Fargate, Docker, Kubernetes, Helm, Karpenter for node autoscaling, "Docker in Action" and "Kubernetes in Action" by Manning.
