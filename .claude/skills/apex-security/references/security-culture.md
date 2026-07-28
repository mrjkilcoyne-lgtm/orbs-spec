# Security Culture

## Scope
Embedding security decision-making and ownership into an organization's values, habits, and incentives so that secure choices are the path of least resistance.

## Core principles
- Security culture is a proxy for compliance, incident rate, and bug severity — cultures that punish reporters or blame individuals have three times higher breach costs (Verizon DBIR); cultures that operationalize learning reduce recurrence.
- Shift the incentive: a culture where finding bugs in code review is praise costs less than a culture where bugs reach prod and someone is blamed; make the discovery a reward, not a punishment.
- Secure-by-default is cheaper than secure-by-choice — defaulted policies (no prod SSH keys in git, MFA required, TLS everywhere) prevent the 95% of mistakes that are carelessness, not malice.
- Security champions embedded in each team (rotating, empowered, connected to the central function) scale what one security expert could never reach and localize decisions to team context.
- Blameless postmortems don't mean "nobody is accountable" — they mean account for the systemic conditions that made the failure likely, not the individual who enacted it; automate away preventable failure modes.

## Apex practices
- Run security training that teaches threat modeling and attack scenarios specific to your product, not checkbox "phishing recognition" — tie it to postmortems and real incidents the company has seen.
- Build security champions as a career path: rotate engineers through the central team, fund them to present at internal conferences, make the rotation a promotion signal, not a tax.
- Operationalize postmortems in code: every serious incident has a ticket with a permanent mitigating test or automated control (e.g., a firewall rule, a regex in SAST) so the same class of mistake cannot recur.
- Require threat modeling and design review only for features crossing trust boundaries or handling new data classes — high signal, low ceremony; skip the 60-slide deck for a new button.

## Pitfalls
- Delegating security to a compliance officer and a box-checking process — security must be every engineer's job or it will not scale.
- Zero-tolerance policies ("get fired if you commit secrets") that incentivize hiding breaches instead of reporting them; invest instead in tooling, education, and automated secrets rotation.
- Training that is mandatory annual compliance theater — 20 minutes of PowerPoint nobody remembers teaches nobody anything; invest in incident-driven learning and communities of practice.

## Tools & references
NIST Cybersecurity Culture Framework, Google's "Rethinking the Security Mindset" (psychological safety framework), Atlassian's "Without Blame" postmortem guide, Blameless (postmortem SaaS), the "Security Champions Network" community model, Shostack on "security poker" (planning games).
