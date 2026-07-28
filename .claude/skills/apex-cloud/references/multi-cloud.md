# Multi-Cloud Strategy

## Scope
Using multiple cloud providers: risk mitigation, vendor lock-in avoidance, and workload-specific optimization.

## Core principles
- Multi-cloud is complex (operational overhead, lack of native integrations, vendor billing opacity) — choose it only for good reasons (avoid lock-in, compliance, risk).
- Portability comes at a cost: using only portable tools (Kubernetes, Terraform) means missing cloud-native features (managed databases optimized for the cloud).
- Data gravity (data is expensive to move) means once you choose a cloud for your data, you're largely committed unless you plan for multi-cloud from day one.
- Compliance and regulatory requirements (data residency, certifications) may force multi-cloud (GDPR in EU, data residency in some countries).
- Operational expertise (skills, tooling, runbooks) doesn't transfer perfectly between clouds; use the same tools (Terraform, Kubernetes) to reduce re-training.

## Apex practices
- Use infrastructure as code (Terraform, Pulumi) with provider-agnostic abstractions (same module generates AWS and GCP) to reduce duplication.
- Standardize on Kubernetes across clouds; run on EKS, GKE, AKS to get portability with cloud-native features.
- Use abstraction layers (app frameworks, libraries) that hide cloud-specific APIs; swap implementations per cloud.
- Implement cross-cloud disaster recovery: data replicated to another cloud, tested regularly, failover procedures documented.

## Pitfalls
- Using multiple clouds without a unified strategy (one team uses AWS, another uses GCP, no standards) — chaos.
- Assuming multi-cloud provides automatic disaster recovery (data doesn't replicate by default; you must explicitly configure it).
- Optimizing for portability over performance (using only generic tools, missing cloud-specific optimizations) — find a balance.

## Tools & references
Terraform, Pulumi, Helm, Kubernetes, cloud-agnostic frameworks, AWS/GCP/Azure documentation, CNCF Cloud Native Landscape.
