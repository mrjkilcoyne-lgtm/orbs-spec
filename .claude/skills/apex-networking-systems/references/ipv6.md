# IPv6

## Scope
IPv6 addressing, SLAAC, DHCPv6, dual-stack deployment, transition mechanisms, and IPv6-specific troubleshooting.

## Core principles
- IPv6 addresses are 128 bits; a /64 prefix is the standard subnet (enough unique hosts for practical purposes), and link-local addresses (fe80::/10) are auto-configured on every interface without DHCPv6.
- SLAAC (Stateless Address AutoConfiguration, RFC 4862) combines RA (Router Advertisement) prefix + interface EUI-64 to auto-configure addresses; no server involvement, but no DHCP-style options — DHCPv6 is needed for DNS/NTP if not in RA.
- IPv6 address types: global unicast (public, like IPv4 public IP), link-local (fe80::, auto-assigned), ULA (unique local, fc00::/7, like RFC1918 private IPs), and multicast (ff00::/8).
- Dual-stack (IPv6 + IPv4 simultaneously) is the transition path; clients prefer IPv6 (getaddrinfo() returns IPv6 first on IPv6-capable systems) but fall back to IPv4; a broken IPv6 stack can block IPv4 via timeouts.
- Neighbor Discovery (ND, ICMPv6) replaces ARP: RS (Router Solicitation) asks for routes, RA answers, NS (Neighbor Solicitation) is "who has X", NA replies; blocking ICMPv6 breaks IPv6 (clients can't find routes or neighbors).

## Apex practices
- Enable IPv6 on all interfaces and test it; many CDNs and services default to IPv6-first now; IPv6-only deployments are becoming real (Salesforce, Facebook Aqua infrastructure).
- Debug with `ip addr show` (see all addresses) and `ip -6 route show` (see IPv6 routes); use `ping6` and `curl -6` to test v6 connectivity; tcpdump filters: `tcp and ipv6`.
- Firewall IPv6 with equal care as IPv4: ip6tables or nftables; don't assume IPv6 is less common and "safe to ignore" — if you advertise it, monitor it.
- Monitor SLAAC/RA behavior with `rdisc6` or `tcpdump -i eth0 icmp6`; confirm clients got valid prefixes with `ip addr show` in the container/VM.

## Pitfalls
- Blocking all ICMPv6 "for security": this disables IPv6 entirely (neighbors can't be resolved, MTU path discovery breaks); fine-tune ICMP rules or disallow only ICMPv6 echo-request.
- Dual-stack where only IPv4 works: clients will hang for ~30 seconds trying IPv6 before falling back (getaddrinfo timeout); test dual-stack before assuming it's backward compatible.
- ULA (fc00::/7) with random prefixes across subnets; use a consistent prefix or none at all (link-local + global unicast is usually enough).

## Tools & references
RFC 4291 (IPv6 Addressing), RFC 4862 (SLAAC), RFC 3315 (DHCPv6); ip, ip6tables, nftables, rdisc6, curl -6, tcpdump -i eth0 icmp6; "IPv6 Essentials" (Huitema/Woodyatt).
