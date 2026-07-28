# SaaS Metrics

## Scope
Subscription-specific metrics used by SaaS companies to measure growth, retention, and health: MRR, ARR, NRR, churn, and expansion.

## Core principles
- Monthly recurring revenue (MRR) is the sum of all active subscriptions in a month annualized and divided by 12; ARR is the same annualized (MRR × 12). Both are backward-looking snapshots, not forward-looking revenue.
- Net revenue retention (NRR) is the gold metric: (beginning MRR + expansion - churn) / beginning MRR, expressed as a percentage; NRR > 100% means existing customers grow even if you add zero new customers (self-funding growth).
- Churn comes in two flavors: logo churn (percentage of customers who leave) and revenue churn (MRR lost); revenue churn can be zero (no customers leave but downgrades offset new logos) — NRR > 100% despite logo churn means upsell is strong.
- SaaS growth = (new ARR added - churned ARR) + (expansion - downgrades); if all three aren't tracked separately, you're blind to which lever is failing.
- Cohort analysis (tracking a group of customers signed in the same month through their lifetime) is non-negotiable; company-level churn hides whether you're getting better at retention or just adding more customers from better channels.

## Apex practices
- Calculate monthly churn and NRR with a 3-month rolling average (one-month churn is noisy); trend matters more than any single month.
- Segment churn by cohort, company size, feature usage, or geography; churn is not uniform — enterprise often has single-digit churn, SMB 5-7%, downmarket 10%+.
- Model payback period improvement from retention engineering; a 1% monthly churn reduction often justifies a major product investment.
- Build a dashboa tracking: MRR growth, new ARR, expansion ARR, churn ARR, and NRR with targets; the mix of growth sources tells you whether the business is sustainable.

## Pitfalls
- Mixing annual and monthly churn; if annual churn is 20%, monthly is ~1.8%, not 20/12 (non-linear).
- Ignoring negative churn (expansion exceeds downgrades); a company with 2% logo churn but 120% NRR is in a different health state than one with identical churn but 95% NRR.
- Using company-level churn as the only signal; if your $1k ARR SMB churn is 10% but $100k ARR enterprise churn is 3%, they're different problems.

## Tools & references
Looker, Amplitude, ChartMogul (SaaS metrics), SaaStr Academy (metrics playbook), Fosbury Financial, Stripe Radar for benchmarks, Reforge SaaS Metrics course.
