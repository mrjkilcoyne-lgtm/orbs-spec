# SAST / DAST

## Scope
Automated security testing: static analysis of source (SAST), dynamic testing of running apps (DAST), plus the adjacent SCA and IAST categories, wired into CI/CD.

## Core principles
- SAST and DAST see different halves of the problem: SAST has full code coverage but no runtime context (high false positives, finds the tainted flow that's actually unreachable); DAST tests real behavior but only on surfaces it can crawl and only for what it can observe — you need both, plus SCA for dependencies.
- Signal-to-noise determines survival: a scanner that cries wolf gets ignored or bypassed within a quarter; ruthlessly tune rulesets, suppress with justification annotations, and track false-positive rate as a first-class metric.
- Dataflow/taint analysis is what separates real SAST (CodeQL, Semgrep taint mode) from glorified grep: source→sanitizer→sink modeling finds injection across function and file boundaries where pattern matching cannot.
- Differential scanning makes CI viable: block merges only on new findings in the diff (fast, fair to the author), while the full-codebase scan runs nightly and feeds a triaged backlog — gating PRs on legacy debt halts delivery.
- Scanners find bug classes with syntactic or behavioral signatures; they are structurally blind to authorization logic, business-logic abuse, and design flaws — that's what threat modeling and manual testing are for.

## Apex practices
- Layer the pipeline: secret scanning + Semgrep on pre-commit/PR (seconds), CodeQL and SCA on merge (minutes), authenticated DAST (ZAP/Burst against staging with a login script) nightly — matching tool cost to feedback-loop position.
- Write custom rules for your own bug classes: every incident or pentest finding becomes a Semgrep/CodeQL rule so the class, not the instance, is fixed ("paved road" enforcement).
- Give DAST authentication and seeded data; an unauthenticated scan of a login wall tests nothing. For APIs, drive DAST from the OpenAPI spec so coverage is enumerable.
- Route findings into the developers' existing workflow (PR comments, Jira) with severity SLAs (e.g., critical fixed < 7 days), and measure mean-time-to-remediate, not finding counts.

## Pitfalls
- Running scanners to generate compliance PDFs while findings rot untriaged — a scanner without a remediation loop is a liability generator.
- Suppressing findings globally (rule disabled repo-wide) instead of per-instance with reason, silently blinding the tool to future real hits.
- Assuming SCA "no known CVEs" means safe dependencies — it says nothing about malicious packages, typosquats, or unmaintained code (that's supply-chain territory).

## Tools & references
Semgrep, CodeQL, SonarQube, OWASP ZAP, Burp Suite, Nuclei, Snyk/Dependabot (SCA), OWASP Benchmark for scanner evaluation, OWASP DevSecOps Guideline.
