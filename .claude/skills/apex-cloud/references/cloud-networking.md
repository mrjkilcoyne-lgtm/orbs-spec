# Cloud Networking

## Scope
Virtual networks, connectivity, and traffic management: VPCs, peering, gateways, and CDN.

## Core principles
- VPC design is foundational — subnets, routing tables, and security groups set boundaries for traffic flow; changes are disruptive later.
- Private subnets (no internet access, NAT egress) are for stateful resources (databases, caches); public subnets (internet-facing) are for stateless services.
- Cross-cloud and on-prem connectivity requires explicit gateways (AWS Direct Connect, GCP Dedicated Interconnect, Azure ExpressRoute) — public internet is not secure for private traffic.
- DNS resolution at scale requires planning (Route53, Cloud DNS) — wildcard records and failover policies prevent hard-coded IPs.
- Network segmentation (security groups, NACLs, policy-based routing) reduces blast radius of a compromise — an attacker in one subnet can't easily pivot.

## Apex practices
- Use VPC peering (same cloud, same region) for low-latency inter-VPC traffic; use VPN or dedicated interconnects for cross-region or cross-cloud.
- Implement network ACLs (stateless) as a coarse filter and security groups (stateful) as a fine filter — defense in depth.
- Use private endpoints (S3, DynamoDB, etc.) to keep traffic off the internet; NAT gateways are more expensive and expose workloads to internet attacks.
- Use DNS failover (health checks + failover routing) to switch traffic between regions or endpoints automatically.

## Pitfalls
- Overly permissive security groups (0.0.0.0/0 for most ports) — lock down to specific sources.
- Single NAT gateway (single point of failure for outbound traffic) — deploy one per AZ.
- No routing policy (static routes only) — implement dynamic routing (BGP) for failover and load balancing.

## Tools & references
AWS VPC, GCP VPC, Azure Virtual Network, Terraform networking modules, DNS RFC 1034, BGP RFC 4271, "Networking in Google Cloud" by Google.
