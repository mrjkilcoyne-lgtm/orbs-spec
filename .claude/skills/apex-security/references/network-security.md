# Network Security

## Scope
Defending the network layer: segmentation, filtering, encrypted transit, DDoS resilience, and detection — on-prem and cloud.

## Core principles
- Segmentation limits blast radius, and its unit has shrunk: from VLANs to security groups to per-workload identity-based policy (Kubernetes NetworkPolicy, service-mesh authorization) — the goal is that compromising one workload buys the attacker reachability to almost nothing (lateral movement is the phase segmentation kills).
- Egress filtering is the underrated control: most breach impact requires calling out (C2 beacons, exfiltration, cryptominers, SSRF to metadata endpoints); default-deny egress with an explicit allowlist breaks whole kill chains that ingress filtering never sees.
- Default-deny is the only rule-set philosophy that scales: allow enumerated flows, deny the rest; allow-by-default plus a blocklist rots into an unauditable mess where nobody dares delete rule 4,000.
- Encrypted transit everywhere means detection moves to metadata and endpoints: flow logs (NetFlow/VPC Flow Logs), DNS query logs, JA3/JA4 fingerprints, and connection-graph anomalies — not payload inspection, which mostly died with TLS 1.3 + ECH.
- DDoS defense is capacity economics: volumetric floods (L3/4, now terabit-scale via amplification and botnets) must be absorbed upstream by anycast scrubbing (Cloudflare, AWS Shield); application-layer (L7) floods need rate limiting, caching, and cost-asymmetry fixes at your edge.

## Apex practices
- Manage network policy as code (Terraform security groups, NetworkPolicy manifests) with review and CI validation; diffable rules with owners and expiry beat console-clicked ones that outlive their reason.
- Log DNS and flow data centrally and alert on the classic tells: DGA-like lookups, DNS tunneling volumetrics, new destinations from stable workloads, port scans from internal hosts.
- Continuously verify exposure from outside: attack-surface scanning of your own ranges and cloud accounts (Shodan/Censys monitoring, scheduled authorized scans) — you want to find the accidentally-public database before someone else does.
- Rehearse DDoS response before you need it: pre-provisioned upstream protection, a runbook with provider escalation contacts, and load-shedding switches you've actually tested.

## Pitfalls
- Hairpinning everything through one inspection choke point that becomes both the availability SPOF and the performance bottleneck — and still misses intra-segment traffic.
- Management planes exposed to the internet: cloud consoles without MFA, SSH/RDP open to 0.0.0.0/0, VPN appliances unpatched (the top initial-access vector class of recent years).
- Treating a private IP as authentication: "it's internal" services with no authn get harvested in the first hour of a lateral-movement campaign.

## Tools & references
Zeek, Suricata, nftables/iptables, VPC Flow Logs, Cilium/Calico NetworkPolicy, WireGuard, Cloudflare/AWS Shield/GCP Cloud Armor, NIST SP 800-207 (for the identity-centric direction), MITRE ATT&CK lateral-movement tactics.
