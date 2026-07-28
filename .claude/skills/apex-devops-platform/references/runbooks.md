# Runbooks

## Scope
Documenting operational procedures: incident response, escalation, recovery steps, and prevention for known failure modes.

## Core principles
- Runbooks are tested procedures, not aspirational documentation — if you haven't run it, it's wrong; runbooks are post-mortems waiting to happen.
- Runbooks enable on-call rotation — a non-expert can follow a runbook to resolve an issue; if the runbook is unclear, the on-call engineer improvises (slow and risky).
- Decision trees beat essays — provide branching logic (if X is true, do Y; if Z is true, do W) so operators don't need to reason about the system.
- Runbooks must include rollback procedures — recovery is not just fixing the symptom, it's restoring the system to a safe state (and understanding what caused the failure).
- Context matters — a runbook is tied to a specific system version, configuration, and set of dependencies; version runbooks like code.

## Apex practices
- Embed runbooks in the codebase (documentation-as-code) so they're reviewed in PRs and versioned with the system.
- Execute runbooks during on-call simulations (game days) monthly or quarterly — discover and fix gaps before incidents.
- Link alerts directly to runbooks ("Page on High Memory Usage" → runbook: "High Memory Usage" with diagnosis and recovery steps).
- Include estimated time-to-resolve (TTR), prerequisites (tools, access, knowledge), and decision logic; format for quick scanning (not paragraphs).

## Pitfalls
- Runbooks written by the engineer who built the system but not reviewed by someone who didn't (they know too much and skip steps).
- No playbook for "what if the runbook is wrong?" (escalation path, who to contact if procedure fails) — unexpected situations require judgment.
- Runbooks specific to one operator (step 3: "login to prod as Alice") — make them generic and reusable by any on-call engineer.

## Tools & references
Runbook templates, postmortem templates, alert documentation, Obsidian or Notion for organization, GitOps-friendly docs in Git, "Site Reliability Engineering" (Google) chapter on playbooks.
