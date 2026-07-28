# Well-Architected Review

## Scope
Assessing cloud architectures against best practices: pillars (operational excellence, security, reliability, performance, cost), trade-offs, and continuous improvement.

## Core principles
- Well-architected is not a state, it's a practice — architectures drift over time; regular reviews (annual, after major changes) catch issues.
- Pillars are not independent; a decision that optimizes cost may hurt reliability — understand trade-offs and choose consciously.
- Baselines (what's good enough?) depend on workload and business goals — a startup can tolerate more risk than a financial institution.
- Automation is the lever for most pillars: infrastructure as code (reproducible), testing (reliable), monitoring (operational excellence).
- Reviews should produce a backlog of improvements; pick the highest-impact, most-feasible items and budget time for them.

## Apex practices
- Use cloud provider frameworks (AWS Well-Architected Framework, GCP's Architecture Framework) for structure; they're comprehensive and regularly updated.
- Hire external reviewers (consultants) for baseline assessments; they bring outside perspective and best practices from other organizations.
- Assign ownership (who's responsible for improving each pillar?) and track progress; without ownership, improvements don't happen.
- Automate checks where possible (IaC linting, security scanning, cost analysis) to catch issues before they're deployed.

## Pitfalls
- Using well-architected as a gate (you must be perfect before deploying) — it should be a guide, not a blocker.
- Optimizing for one pillar at the expense of others (maximum security with no performance = no users) — balance trade-offs.
- One-time review without follow-up; architecture drifts and gets worse over time.

## Tools & references
AWS Well-Architected Framework, GCP Architecture Framework, Azure Well-Architected, Infrastructure automation tools, CNCF Cloud Native Landscape, architecture review tools.
