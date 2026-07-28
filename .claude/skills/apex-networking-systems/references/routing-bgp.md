# Routing & BGP

## Scope
How packets find paths: IGPs (OSPF/IS-IS) inside a network, BGP between autonomous systems, and the operational realities of interdomain routing.

## Core principles
- BGP is a policy protocol, not a shortest-path protocol: route selection walks local-pref → AS-path length → origin → MED → eBGP-over-iBGP → IGP cost → tiebreakers, and money (peering vs transit economics) usually decides local-pref before topology gets a vote.
- BGP trusts by default: any AS can announce any prefix, so hijacks and fat-finger leaks (Pakistan/YouTube 2008, Facebook's 2021 withdrawal self-outage) are structural risks; RPKI route-origin validation and prefix filtering are the deployed mitigations.
- Longest-prefix match always wins — announcing a /24 out from under someone's /16 steals the traffic; this is both the hijack mechanism and the standard traffic-engineering knob.
- Convergence is not instant: BGP path hunting after a withdrawal can take minutes globally; design for the transient (anycast helps, as does not flapping — route-flap damping penalizes unstable announcements).
- Inside an AS, iBGP requires a full mesh or route reflectors, and next-hop reachability comes from the IGP — most "BGP is broken" incidents inside a network are actually IGP or next-hop-resolution problems.

## Apex practices
- Filter aggressively at every eBGP boundary: max-prefix limits, bogon and RFC 1918 filters, AS-path sanity, and IRR/RPKI-based prefix lists per peer — most leaks are stopped by the neighbor's filters, not the leaker's discipline.
- Sign ROAs for your prefixes and drop RPKI-invalid routes; monitor your prefixes with external viewpoints (RIPE RIS, RouteViews, BGPStream, commercial monitors) so you learn about a hijack before your customers do.
- Traffic-engineer with the standard toolkit: prepend AS-path to deprioritize a link, split announcements into more-specifics for inbound control, use communities your transit providers publish for selective propagation.
- Follow MANRS norms; validate config changes against a lab or `bgpq4`-generated filters before touching production sessions, and always have out-of-band access — you cannot fix BGP over the path BGP just killed (Facebook 2021's lesson).

## Pitfalls
- Leaking full tables or provider routes to peers because a filter defaulted to permit-any — the classic route-leak that turns a small AS into accidental transit and melts its links.
- Forgetting that outbound announcements steer inbound traffic and vice versa; prepending affects how others reach you, not how you reach them.
- Treating BGP timers/BFD as free: aggressive hold timers without BFD flap sessions on lossy links, and each flap triggers global reconvergence and damping penalties.

## Tools & references
RFC 4271 (BGP-4), RFC 6811 (RPKI origin validation), MANRS; BIRD, FRRouting, GoBGP; RIPE RIS/RIPEstat, RouteViews, bgp.tools, "Internet Routing Architectures" (Halabi).
