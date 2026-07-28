# AWS Core

## Scope
Fundamental AWS services and architectural patterns: EC2, VPC, IAM, autoscaling, and regional/multi-region design.

## Core principles
- AWS regions are independent — data doesn't replicate across regions by default, resilience requires explicit multi-region design.
- EC2 instances are ephemeral; treat them as cattle, not pets — instances fail, disks are unreliable, use S3 and EBS for durable storage.
- VPC design sets the foundation for security and scalability — subnets, routing, security groups, and NACLs require up-front planning; changes are disruptive later.
- IAM is granular and complex; overpermissioning is the norm — enforce least privilege with regular audits (IAM Access Analyzer), assume roles instead of long-lived keys.
- Autoscaling is a behavior, not a button — define what triggers scaling (CPU, custom metrics, scheduled), set min/max replicas, and test failure modes.

## Apex practices
- Use VPC endpoints for AWS services (S3, DynamoDB, SNS) to avoid internet gateway and NAT costs — traffic stays within AWS network.
- Implement multi-AZ (availability zone) redundancy for critical resources (databases, load balancers, NAT gateways); single-AZ is a single point of failure.
- Use instance types that match your workload: compute-optimized for CPU-bound, memory-optimized for caching, graviton (ARM) for cost, spot for batch.
- Enforce tagging discipline (cost center, environment, owner) at creation time via IAM policies or SCPs (Service Control Policies); untagged resources are blind spots.

## Pitfalls
- Treating one AZ as sufficient for anything critical (an AZ fails, your workload goes down) — always multi-AZ.
- Using default VPCs and security groups permissive to 0.0.0.0/0 (anyone can attack) — lock down from day one.
- Autoscaling on CPU metrics in bursty workloads (scales after the spike has passed) — use custom metrics or request count instead.

## Tools & references
AWS Well-Architected Framework, AWS documentation, Terraform AWS provider, cdktf, "AWS for Everyone" by Forrest Brazeal.
