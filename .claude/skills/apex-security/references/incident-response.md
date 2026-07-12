# Incident Response

## Scope
Detecting, containing, eradicating, and recovering from security incidents, and building the organizational machinery that makes response fast and repeatable.

## Core principles
- The lifecycle is NIST SP 800-61: preparation → detection & analysis → containment, eradication & recovery → post-incident activity; the quality of the first phase (playbooks, access, logging, contacts, practice) determines the speed of all the others.
- Containment before eradication, scoping before containment: wiping the first compromised host you find alerts the adversary and destroys evidence while their three other footholds persist — scope the intrusion (IOC sweep, timeline), then contain everything at once.
- Assume-breach math: the metrics that matter are dwell time, mean-time-to-detect, and mean-time-to-contain; attackers move laterally within hours (CrowdStrike's "breakout time" averages under 90 minutes), so a detection pipeline with day-long alert queues has already lost.
- Credential invalidation is the heart of most modern containment: session revocation, key rotation, OAuth grant revocation, forced password resets — because most intrusions run on stolen or minted credentials, not malware.
- Decision authority must be pre-assigned: who can take prod down, who talks to lawyers/regulators/customers, who declares severity — deciding this during the incident costs the hours that matter (GDPR gives you 72 to notify).

## Apex practices
- Write playbooks per incident class (compromised credentials, ransomware, exposed secret, malicious insider, vendor breach) with concrete first-hour checklists, and run tabletop exercises quarterly — the playbook you've never rehearsed is fiction.
- Preserve before you fix: snapshot disks/memory, export logs beyond retention windows, record timestamps and actions in an incident log as you go — legal, insurance, and the postmortem will all need it.
- Instrument for the questions you'll ask: centralized logs with retention ≥ 90 days hot / 1 year cold, authentication events, cloud control-plane audit trails (CloudTrail et al.), and EDR on endpoints — you can't investigate what you didn't record.
- Run blameless post-incident reviews that produce systemic fixes (detection gaps closed, playbook diffs, control changes) with owners and deadlines; count recurrence of the same root cause as the failure metric.

## Pitfalls
- Alerting the adversary mid-scoping: mass password resets or blocking their C2 before you've mapped their access invites them to burn the environment or deploy backup persistence.
- Communicating about the incident inside the compromised environment — if the attacker reads your email/Slack, they're reading your response plan; have an out-of-band channel ready.
- Declaring victory after eradication without hardening the initial-access vector — re-compromise via the same door within weeks is a well-documented pattern.

## Tools & references
NIST SP 800-61r2, SANS Incident Handler's Handbook, MITRE ATT&CK (scoping vocabulary), TheHive/Cortex, Velociraptor, GRR, PagerDuty/incident.io for coordination, CISA incident response playbooks.
