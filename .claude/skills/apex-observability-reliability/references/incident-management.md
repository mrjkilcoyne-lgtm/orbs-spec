# Incident Management

## Scope
Detecting, triaging, responding to, and communicating about incidents; coordination across teams and customer notification.

## Core principles
- Incident severity (1-5, or SEV1-5) drives response: SEV1 is total outage, SEV2 is degradation affecting many users, SEV3 is edge cases or minor impact.
- Triage (assessment within 5 minutes) determines severity, scope (which services/customers are affected), and remediation strategy (rollback vs. fix forward).
- Incident commander (a single person coordinating response) prevents communication chaos; without one, multiple people investigate in parallel and miscommunicate.
- Customer communication (status page updates, email) is separate from technical response; inform customers even if you don't know the fix yet.
- Blameless postmortems (analyzing what happened, not who caused it) are the only path to learning; blaming individuals kills incident reporting.

## Apex practices
- Detect incidents automatically (alerting, synthetic monitoring) rather than waiting for customer complaints; MTTR is 10x longer if detection is manual.
- Create an incident channel (Slack, Teams) with all relevant parties (engineering, product, support, comms) to centralize information.
- Keep a timeline: log actions, context changes, and observations in real-time; this is the basis for the postmortem.
- Declare an incident early and publicly; saying "we're investigating a potential issue" is better than silence.

## Pitfalls
- No clear severity definition; is a 1% user impact SEV1 or SEV3? Ambiguity leads to mismatched responses.
- Incident commander who is also debugging (cognitive overload); separate the roles.
- Post-incident blame; "who deployed this?" instead of "what systemic issue allowed this?"

## Tools & references
PagerDuty, Opsgenie, Incident.io, Atlassian StatusPage, Google Incident Response Guide, VictorOps Incident management best practices, blameless incident postmortems (Etsy's John Allspaw, Google SRE Book).
