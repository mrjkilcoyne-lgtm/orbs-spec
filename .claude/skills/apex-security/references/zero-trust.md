# Zero Trust

## Scope
The architecture that replaces network-location trust with continuous, identity-centric, per-request authorization — for users, devices, and workloads.

## Core principles
- The core axiom (NIST SP 800-207): no implicit trust from network position; every access is authenticated, authorized, and encrypted per-request, evaluated against identity, device posture, and context — "internal network" stops being a permission.
- The historical driver is lateral movement: perimeter models fail open once one host or credential is compromised (every major breach narrative); zero trust makes each resource its own perimeter so one foothold buys almost nothing.
- The policy engine / policy enforcement point split is the architecture: a decision service evaluates (subject, device, resource, context) against policy; distributed enforcement points (proxies, gateways, sidecars) apply it — BeyondCorp is the canonical worked example (Google's papers, 2014-2016).
- Trust is continuous, not a session event: signals (device compliance drift, impossible travel, session anomalies, token age) can downgrade or revoke access mid-session; authentication at 9am must not authorize at 5pm unconditionally.
- Workloads need identity as much as users: service-to-service trust via mTLS with SPIFFE-style short-lived certificates and per-service authorization policy — IP allowlists and flat cluster networks are perimeter thinking indoors.

## Apex practices
- Sequence pragmatically: strong IdP with phishing-resistant MFA and SSO everywhere → device inventory + posture (MDM/EDR signals) → put apps behind an identity-aware proxy (retiring VPN-wide access) → microsegment east-west traffic → continuous signal evaluation. Each phase pays for itself.
- Kill standing privilege: just-in-time, just-enough access with expiry for admin operations (short-lived credentials from a broker), so "who can touch prod right now" is a small, auditable, time-boxed set.
- Start with the crown jewels and new systems rather than boiling the whole estate; a zero-trust path to your most sensitive app delivers more risk reduction than a half-migrated everything.
- Log every access decision (allow and deny) with full context; the decision log is simultaneously your audit trail, your anomaly-detection feed, and your policy-debugging tool.

## Pitfalls
- Buying "a zero trust product" and declaring the transformation done — it's an operating model spanning identity, device, network, and app layers; a ZTNA gateway in front of unchanged flat networks is a nicer VPN.
- Policy so aggressive it breaks workflows on day one, generating exception sprawl that quietly reconstructs implicit trust; roll out in report-only mode and ratchet.
- Forgetting non-interactive identities: service accounts, CI tokens, and API keys with static credentials and no posture checks become the softest path in — they need the same lifecycle rigor as humans.

## Tools & references
NIST SP 800-207, Google BeyondCorp papers, CISA Zero Trust Maturity Model, SPIFFE/SPIRE, identity-aware proxies (Cloudflare Access, Tailscale, Pomerium), service mesh authz (Istio), Kindervag's original Forrester "No More Chewy Centers."
