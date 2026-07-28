# Security Testing Concepts

## Scope
Authorized offensive-style validation of defenses: penetration testing, red team exercises, purple teaming, and bug bounty programs — how mature organizations use them, ethically and under explicit authorization.

## Core principles
- Authorization is the line between security testing and crime: written scope, rules of engagement, time windows, emergency contacts, and (for third parties) contracts — the CFAA and equivalents don't care about intent, and testers carry the "get out of jail" letter for a reason.
- The forms answer different questions: vulnerability assessment asks "what's exposed" (breadth, scanner-driven), penetration testing asks "can this scope be broken and how far" (depth, human-driven, weeks), red teaming asks "does our detection & response actually work against a realistic adversary" (stealth, objectives-based, blue team unaware).
- A pentest is a sample, not a proof: it demonstrates the presence of exploitable weakness, never the absence; a clean report bounded by two weeks and one scope means exactly that.
- Realism drives red team value: emulate relevant adversaries using ATT&CK-mapped TTPs and frameworks like TIBER-EU or CBEST; the deliverable is detection gaps and response-timing data, not a trophy shell.
- The kill chain is a defensive model: recon → initial access → persistence → privilege escalation → lateral movement → objective; each phase is a detection and disruption opportunity, and exercises should measure at which phase the defense caught (or missed) the operator.

## Apex practices
- Purple-team the findings: run attack technique, observe telemetry, tune detection, re-run until caught — turning offensive knowledge directly into detection engineering (map coverage in ATT&CK Navigator).
- Treat findings as classes: every pentest finding gets a root-cause fix (the pattern, via paved-road tooling or policy) plus a regression test, not just the instance patched; retest to verify.
- Scope tests where risk lives: new attack surface, recently changed auth flows, tenant isolation, and the crown-jewel paths from your threat model — not the same perimeter scan annually for compliance.
- Run bug bounty/VDP as a funnel with SLAs: clear scope and safe-harbor language, fast triage, payment tied to impact — a well-run program is continuous testing; a badly-run one trains researchers to go elsewhere.

## Pitfalls
- Testing production without blast-radius planning: DoS-ing prod with a scanner, exfiltrating real customer data as "proof," or social-engineering staff outside agreed rules — scope discipline is part of professional competence.
- Shelfware reports: findings without owners, severity inflation/deflation negotiations, and the same critical reappearing three years running.
- Red teaming before you have detection to test: if there's no SOC/telemetry, you'll pay for an expensive demonstration that stealth works — spend on detection first, red team to validate it.

## Tools & references
MITRE ATT&CK & Navigator, PTES, OWASP WSTG, NIST SP 800-115, TIBER-EU/CBEST, Atomic Red Team & Caldera (adversary emulation), HackerOne/Bugcrowd, PortSwigger Academy for skill-building.
