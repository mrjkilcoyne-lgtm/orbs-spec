# VPN & Tunneling

## Scope
Encrypted overlays and encapsulation: WireGuard, IPsec, OpenVPN, mesh VPNs (Tailscale-style), and generic tunneling (GRE, VXLAN, SSH) with their MTU and routing consequences.

## Core principles
- Every tunnel spends MTU: encapsulation overhead (WireGuard 60 bytes on IPv4, IPsec ~50-73, VXLAN 50) shrinks the effective payload below 1500, and if PMTUD is broken you get the signature "small packets work, big transfers hang" — clamp MSS or set tunnel MTU explicitly (WireGuard's 1420 default exists for this reason).
- WireGuard's design lesson is that less is more: ~4k lines, one modern cipher suite (Noise/ChaCha20-Poly1305, Curve25519), no negotiation, identity = static public key. No cipher agility means no downgrade attacks — contrast IPsec's IKE combinatorics where most failures are proposal mismatches.
- A VPN moves the trust boundary, it doesn't create security: once inside the tunnel you're on the network — pair tunnels with per-service authentication and least-privilege routing (allowed-ips in WireGuard is a routing ACL, not just routing).
- Routing decides what the tunnel means: full-tunnel (default route via VPN) vs split-tunnel (specific prefixes) is a security-vs-performance policy choice; the kernel routing table, not the VPN daemon, determines which packets enter the tunnel.
- TCP-over-TCP is pathological: two stacked retransmission/congestion loops amplify each other under loss (meltdown); prefer UDP transports (WireGuard, OpenVPN-UDP, IPsec/ESP) and treat TCP:443 transport as a last-resort firewall-traversal mode.

## Apex practices
- Mesh over hub-and-spoke for peer-to-peer traffic: modern mesh VPNs do NAT traversal (STUN-style endpoint discovery, UDP hole punching) with relay fallback (DERP/TURN), removing the central chokepoint and its RTT tax.
- Keep NAT mappings alive deliberately: WireGuard `PersistentKeepalive = 25` for peers behind NAT; without it, inbound packets after idle silently vanish and "VPN randomly disconnects" tickets appear.
- Verify the tunnel is actually used: `ip route get <dst>`, `tcpdump -i wg0` vs the physical interface, and check for leaks (DNS queries and IPv6 traffic bypassing an IPv4-only tunnel are the two classic leak paths).
- Automate key lifecycle: distribute WireGuard peers from config management or a coordination plane, rotate on personnel change, and never reuse a private key across devices — the key is the identity.

## Pitfalls
- MTU mishandling: leaving tunnel MTU at 1500, or nesting tunnels (VPN over VXLAN over PPPoE) until effective MTU is tiny and nothing fragments correctly; always test with `ping -M do -s <size>`.
- Overlapping address space: connecting two sites that both use 10.0.0.0/8 — traffic can't route unambiguously; plan address allocation before connecting networks or you'll live with NAT band-aids forever.
- IPsec/IKE misconfig archaeology: mismatched phase 1/2 proposals, NAT-T not enabled, or one side rekeying with different lifetimes causing periodic drops exactly at the SA lifetime boundary — the period of the failure is the diagnostic.

## Tools & references
WireGuard whitepaper (Donenfeld, NDSS 2017), RFC 4301 (IPsec), RFC 7296 (IKEv2); wg/wg-quick, strongSwan, OpenVPN, Tailscale/Headscale docs; tcpdump on both tunnel and physical interfaces.
