# NAT & Proxies

## Scope
Network Address Translation, proxy patterns (L4/L7), connection tracking, NAT traversal, and address rewriting for service discovery and routing.

## Core principles
- NAT rewrites source/destination addresses and ports in packet headers; stateless NAT (rare) is simple but unusable; stateful NAT (conntrack) tracks tuples and must reverse rewrites on reply — the table size limits connection count.
- Netfilter/nftables connection tracking (conntrack) manages state in memory: each TCP connection is a conntrack entry (300 bytes, ~1 million per GB); table overflow (NFCT quota) causes new connections to fail with no error.
- L4 load balancing (DSR/direct server return) avoids the reverse path: replies bypass the LB and go straight to client, halving LB bandwidth — requires the backend to accept packets from client IPs (ARP spoofing locally, or static routes).
- L7 proxies (HTTP, gRPC) see and can modify payload: they're application-aware, can route on path/host, but add latency and are a scaling bottleneck; connection pooling and keepalive are essential.
- Port exhaustion is real: clients making short connections to one server use up 65k ports (65k - 1024 max) in ~10 seconds; NAT/LB connection reuse or SO_REUSEADDR help, but the limit is fundamental.

## Apex practices
- Monitor conntrack table with `/proc/net/nf_conntrack` or conntrack -L; size NFCT_MAX via nf_conntrack_max to match your connection rate; aim for <50% full at peak.
- Use SO_REUSEADDR + TCP_TIMESTAMP to reuse TIME_WAIT ports (tcp_tw_reuse); verify it's safe for your protocol (retransmits after close are rare but possible).
- For service discovery behind NAT, use DNS or service mesh (Envoy, Istio) rather than bare IP:port; automatic VIP (virtual IP) assignment and health checks are essential.
- Debug with `tcpdump -i any 'host X'` across the NAT boundary; compare source IPs in packets on each side to confirm rewriting; use `conntrack -E` to watch state transitions.

## Pitfalls
- Conntrack table overflow silently dropping new connections; customers see "connection refused" without clear cause; set up alerting on `nf_conntrack_count / nf_conntrack_max`.
- Forgetting that UDP conntrack times out ~30 seconds idle; protocols with infrequent packets need application-level keepalives or DNS re-resolution.
- L7 proxy single points of failure; always run at least 2 instances with health checks and fast failover.

## Tools & references
netfilter/nftables documentation, conntrack-tools, iptables-save, tcpdump, Envoy/HAProxy/nginx as L7 proxies; "Linux iptables Pocket Reference" (Greear); conntrack kernel module parameters.
