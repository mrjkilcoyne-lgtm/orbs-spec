# Error Budgets

## Scope
Spending tolerance within SLOs: tracking error budget consumption, pausing features during deficit, and balancing velocity with reliability.

## Core principles
- Error budget is how much you can deviate from SLO before breaching it: if SLO is 99.9% uptime, budget is 0.1% of time (43 seconds per month).
- Spending error budget is an investment in velocity: shipping features faster (risky deployments, skipped tests) burns budget faster but enables more velocity.
- Error budget policies determine behavior: if you exceed budget, pause risky changes and focus on stability until you're back in budget.
- Budget can be spent on deployments, experiments, or incidents; all contribute equally to deviation from SLO.
- Error budget is not a license to break things; it's a shared resource between product (velocity) and engineering (reliability).

## Apex practices
- Track error budget daily and project to end of month; if you're on pace to exceed budget, take action now.
- Publish error budget dashboards to product and engineering; shared visibility prevents surprises.
- Set a policy: when error budget is 50% spent, reduce deployment frequency or pause risky experiments.
- Use error budget for deliberate trade-offs: "we'll run an aggressive experiment this week and burn 20% of budget because the upside is worth it."

## Pitfalls
- Treating error budget as punishment ("you spent the budget, now you have to fix reliability"); it's a shared resource for making trade-offs.
- Not tracking error budget accurately; if you can't measure your SLI reliably, you can't track budget.
- Over-spending early and then being paralyzed by lack of budget; distribute decisions throughout the month.

## Tools & references
Google SRE Book (error budget chapters), Datadog error budget tracking, New Relic, error budget policies (Liatrio), error budget burn dashboard examples.
