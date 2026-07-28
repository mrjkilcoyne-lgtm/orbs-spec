# Threat Modeling

## Scope
Systematically identifying what can go wrong in a design before it ships: assets, attackers, attack surfaces, and mitigations.

## Core principles
- Answer Shostack's four questions: what are we building, what can go wrong, what are we doing about it, did we do a good job — a model that skips any of them is decoration.
- Threats live on data flows crossing trust boundaries; draw the DFD first and every arrow that crosses a boundary (browser→API, service→DB, tenant→tenant) is where STRIDE gets applied.
- STRIDE gives per-element coverage: Spoofing hits identities, Tampering hits data flows and stores, Repudiation hits logging, Information disclosure hits stores, DoS hits everything, Elevation of privilege hits processes.
- Rank with impact × exploitability, not raw counts: a low-effort unauthenticated RCE outranks fifty authenticated low-severity findings; DREAD-style scoring is fine as long as the team applies it consistently.
- The model is a living artifact tied to the design: re-run it when a trust boundary moves (new integration, new tenant model, new data class), not on a calendar.

## Apex practices
- Timebox to 60–90 minutes per feature with the engineers who built it in the room — a rough model by the team beats a perfect one by a distant security team.
- Turn every accepted threat into a tracked ticket with an owner and a mitigation or an explicit risk acceptance signed by someone with authority to accept it.
- Use attack trees for the top 2–3 scary scenarios ("attacker exfiltrates all tenant data") to find the cheapest attacker path — that path gets the mitigation budget.
- Keep an abuse-case suite: encode modeled threats as automated tests (IDOR probes, boundary fuzzing) so regressions in mitigations are caught in CI.

## Pitfalls
- Modeling the network diagram instead of the data flows — threats follow data, and a "hardened perimeter" model misses the insider and the compromised dependency.
- Producing a 40-page document nobody updates; six months later the architecture has changed and the model actively misleads.
- Only modeling malicious outsiders — forgetting compromised credentials, malicious insiders, and confused-deputy paths between your own services.

## Tools & references
Shostack's "Threat Modeling: Designing for Security," OWASP Threat Dragon, Microsoft Threat Modeling Tool, STRIDE, attack trees (Schneier), the Threat Modeling Manifesto.
