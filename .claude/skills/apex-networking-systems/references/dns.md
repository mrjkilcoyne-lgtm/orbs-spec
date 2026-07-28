# DNS

## Scope
The Domain Name System: hierarchy, resolution paths, record types, caching, DNSSEC, and DNS as an availability and traffic-steering layer.

## Core principles
- Resolution is a delegation walk: recursive resolver → root → TLD → authoritative, with caching at every hop governed by TTL; the resolver's cache — not your zone file — is what clients actually experience, so a change propagates over max(TTL) not instantly.
- CNAME rules are strict: no CNAME at a zone apex (it must coexist with SOA/NS, which is forbidden), which is why ALIAS/ANAME flattening exists; a CNAME chain also adds a lookup per link.
- Negative caching (RFC 2308) means NXDOMAIN answers are cached per the SOA minimum — a typo'd record can keep "not existing" for hours after you fix it.
- DNS is the oldest global eventually-consistent database: design deploys around it (lower TTLs to 60 s a day before a migration, raise them after) rather than fighting it.
- DNSSEC signs data (authenticity), while DoT/DoH encrypt transport (privacy) — they solve different problems; a signed-but-plaintext answer is still visible, an encrypted-but-unsigned one is still spoofable by the resolver.

## Apex practices
- Debug with `dig +trace` (walks delegation from root, bypassing caches) and `dig @specific-server` to isolate which layer disagrees; compare authoritative answer vs your recursive resolver's cached one before touching anything.
- Treat DNS as a failover and steering primitive with eyes open: health-checked records (Route 53-style) fail over in TTL time at best, and some resolvers ignore low TTLs — pair DNS steering with anycast or client retry for real availability.
- Monitor for the classics: expiring domain registrations, expiring DNSSEC signatures (RRSIG), and lame delegations — each has caused headline outages (e.g., Slack's 2021 DNSSEC incident).
- Keep NS TTLs long and stable, delegate subdomains to isolate blast radius, and never point production records at IPs you don't control the lifecycle of (dangling CNAME/A records are a subdomain-takeover vector).

## Pitfalls
- Believing "we lowered the TTL an hour ago, we're safe" — resolvers that cached the record before the change still hold the old TTL; the lowering itself propagates over the old TTL.
- Forgetting that clients, OS stub resolvers, browsers, and Java runtimes each add their own caching layer with their own (sometimes infinite — old JVM default) TTL policy.
- Round-robin A records as load balancing: no health awareness, resolver reordering is inconsistent, and one dead IP takes out a fraction of users for a full TTL.

## Tools & references
RFC 1034/1035, RFC 2308, RFC 4033-4035 (DNSSEC); dig, kdig, dnsviz.net, Zonemaster; "DNS and BIND" (Liu & Albitz), PowerDNS/Unbound/CoreDNS docs.
