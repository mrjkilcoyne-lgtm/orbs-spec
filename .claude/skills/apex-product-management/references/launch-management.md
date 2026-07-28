# Launch Management

## Scope
Coordinating the go-live of a product or significant feature: sequencing, stakeholder prep, rollout strategy, and customer enablement.

## Core principles
- A launch is not the day the button ships; it spans from announcement through adoption adoption curve inflection (day 30-90). Shipping the code is day 1, not day 0.
- Launches require active leadership alignment before execution: sales team knows the talking points, support is trained, customer success has the onboarding flow, marketing has the narrative; silent launches are ship misses.
- Rollout sequencing matters more than global launch: land with power users or a wedge segment first (validates the product, generates case studies), then broaden. A botched launch with 1% of traffic is fixable; with 100% it's a crisis.
- The launch plan must include the abort plan: what's the rollback? How many hours of downtime tolerance before we revert? If the answer is "undefined," the launch is not ready.
- Launch velocity trades against launch coverage: ship small and often and learn, or ship big once and live with the consequences. Pick one per quarter; mixing creates whiplash.

## Apex practices
- Create a launch playbook per launch type (API endpoint, dashboard feature, billing model change) with checklists for sales, support, customer success, and marketing; the repetition surfaces forgotten steps.
- Run a customer advisory board preview (or beta with 5-10 power users) 3 weeks before general availability; their friction becomes your documentation and talking points.
- Stagger the rollout: start with internal (dogfooding catches bugs), then beta (control group for metrics), then 10% canary (catch tail latency issues), then 50%, then 100%; each stage is a gate.
- Measure launch health with leading indicators (adoption curve vs. baseline, support ticket spike, feedback sentiment) not just trailing indicators (revenue impact after 90 days).

## Pitfalls
- Planning the launch after the feature is code-complete; launch strategy should inform feature scope (if you can't land it in stages, you shipped the wrong thing).
- Over-communicating the launch and creating expectation debt that the feature can't repay; undersell, over-deliver.
- Treating rollback as failure; rollback is optionality. "We shipped it, broke it, rolled it back, fixed it, launched it again" is success.

## Tools & references
LaunchDarkly (progressive deployment), feature flag best practices (Etsy, GitHub), customer beta programs (Doerr's launch frameworks), PostHog (rollout analytics), Pagerduty (incident management during launch).
