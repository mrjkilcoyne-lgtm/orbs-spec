# Firewalls

## Scope
Packet filtering and policy enforcement: Linux netfilter (iptables/nftables), stateful connection tracking, cloud security groups, and firewall policy design.

## Core principles
- Stateful beats stateless: conntrack tracks connection state (NEW/ESTABLISHED/RELATED) so policy reduces to "allow NEW inbound on these ports, allow ESTABLISHED both ways" — without state you must reason about both directions of every flow and TCP flag combinations.
- Default-deny is the only defensible posture: enumerate what's allowed, drop the rest, and log the drops; a default-allow firewall with block rules is a list of yesterday's incidents.
- Rule order and first-match semantics mean a firewall is a program: an early broad accept shadows every later rule, and iptables evaluates linearly (nftables uses maps/sets for O(1) lookups — meaningful at thousands of rules).
- The conntrack table is a finite resource and an attack surface: `nf_conntrack_max` overflow silently drops new connections, and every NAT box or stateful firewall in the path is a place idle connections die (typical cloud/NAT idle timeouts: 350 s AWS NAT GW, 4 min Azure LB) — hence TCP keepalives below the timeout.
- DROP vs REJECT is a real choice: REJECT (RST/ICMP unreachable) gives fast, debuggable failures inside your network; DROP makes clients hang until timeout and is mainly useful at the internet edge to slow scanners.

## Apex practices
- Write policy as intent, not addresses: use nftables named sets / ipsets / cloud security-group references so "app tier can reach db tier on 5432" survives IP churn; regenerate from source of truth (IaC) rather than hand-editing live rules.
- Stage risky changes with a dead-man switch: `sleep 300 && nft flush ruleset`-style auto-rollback (or `iptables-apply`) before applying rules over SSH on a remote box.
- Log with rate limits and structure (`nft ... log prefix "denied-inbound " limit rate 5/second`) and actually ship those logs — denied-traffic patterns are your cheapest intrusion telemetry.
- Test the policy from outside: nmap the box from an untrusted vantage point after changes; the ruleset you think you applied and the reachability that exists are verified independently.

## Pitfalls
- Locking yourself out: applying a default-deny before the SSH allow rule, or flushing rules with the default policy set to DROP — always have console/OOB access and a rollback timer.
- Forgetting non-TCP realities: blocking all ICMP breaks PMTUD (black-holed big packets) and IPv6 entirely (ICMPv6 is mandatory — ND, PMTUD); blocking UDP breaks DNS, QUIC, WireGuard.
- Duplicated policy layers drifting apart: host firewall says one thing, security group another, network ACL a third — the effective policy is the intersection, and debugging requires checking all of them.

## Tools & references
nftables wiki, iptables/conntrack man pages, RFC 4890 (ICMPv6 filtering); nmap, nft monitor, conntrack -L; cloud SG/NACL docs; firewalld/ufw as frontends.
