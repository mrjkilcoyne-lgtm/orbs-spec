# CI/CD (Continuous Integration and Delivery)

## Scope
Automating build, test, and deployment pipelines to reliably move code from commit to production with minimal human intervention.

## Core principles
- CI/CD is the primary feedback loop for code quality; broken builds must be visible and actionable within seconds, not hours.
- Every commit flows through the same CI pipeline that runs on main — divergent paths hide integration issues; consistency across branches reveals them.
- Fast feedback beats comprehensive feedback: run smoke tests and security scans in the critical path (~5 min), push slow tests (load, integration) to post-merge or nightly gates.
- Deployment stages (dev→staging→prod) should be identical except for config — build once, promote the artifact; rebuilding is a source of bugs.
- Rollback must be faster and more reliable than deploy; if rollback is scary, your deploy isn't ready.

## Apex practices
- Gate merges on CI results (branch protection), not trust — enforce required status checks and require PRs to be up-to-date with main before merge.
- Parallelize independent build stages (compile, unit tests, lint, SAST) and cache dependencies aggressively to keep critical path under 5 minutes.
- Capture and surface CI logs and artifacts clearly; a dev spending 10 minutes debugging a cryptic build error should have better output.
- Implement staged rollout to canary deployments automatically — deploy to 5% first, compare metrics against baseline (latency, error rate, custom signals), then 50%, then 100%.

## Pitfalls
- Treating CI as a report-only gate with no teeth — a red build that sits ignored becomes the default.
- Sequential CI stages (build, then test, then lint, then deploy) — parallelization drops wall-clock time by 60%+ for the same coverage.
- Not testing the deployment pipeline itself — your blue-green cutover is untested until production, when failure is public.

## Tools & references
GitHub Actions, GitLab CI, Jenkins, CircleCI, ArgoCD for GitOps CD, CNCF Continuous Delivery survey.
