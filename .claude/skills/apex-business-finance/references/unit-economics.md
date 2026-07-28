# Unit Economics

## Scope
The per-customer or per-transaction profitability of a business: customer acquisition cost (CAC), lifetime value (LTV), payback period, and margins.

## Core principles
- LTV-to-CAC ratio (LTV ÷ CAC) must exceed 3:1 to be sustainable (lower than 3 means you're spending more to acquire than you'll ever make); venture benchmarks are 5:1+, mature SaaS is 8-10:1.
- CAC payback period (months of revenue needed to recoup the acquisition cost) should be less than 12 months for efficient SaaS; if it takes 24 months, you're dependent on retention compounding and vulnerable to churn.
- LTV calculation depends on pricing model: for subscription, LTV = ARPU × gross margin % × (1 / monthly churn rate), sometimes adjusted for retention curves; for transactional (e-commerce), it's cumulative profit per customer across repeat purchases.
- Unit economics are per-cohort, not per-company average: a customer acquired in Jan 2022 cohort has different LTV than Jan 2023 if pricing or churn changed; cohort analysis reveals deterioration.
- Contribution margin (revenue minus cost of goods sold, excluding overhead) must be positive per unit for growth to be efficient; companies with negative contribution margins are accelerating losses, not revenue.

## Apex practices
- Track CAC by channel and payback period; if organic has 6-month payback and paid search has 18-month payback, allocate more to organic.
- Model multiple LTV scenarios (25th percentile churn, median, 75th) and run sensitivity on retention improvements; a 1-2% reduction in churn often doubles LTV.
- Calculate blended unit economics (time-weighted or revenue-weighted average across all customer cohorts); single cohort economics can hide declining efficiency.
- Build a unit economics dashboard updated monthly; LTV deterioration (slower payback, higher churn) is a leading indicator of growth stalls that P&L lags by quarters.

## Pitfalls
- Calculating LTV using only first-year revenue (incorrect denominator); the right denominator includes all cash the customer generates until they churn or die.
- Ignoring churn and treating LTV as a fixed multiple of ARPU; high-churn businesses have LTV that improves dramatically with retention engineering.
- Paying attention to CAC but not profitability; an efficient CAC is worthless if gross margins are 20% (you'll never achieve 3:1 LTV-to-CAC).

## Tools & references
Fosbury Financial (SaaS metrics), SaaStr benchmark reports, Twitch metrics dashboard (public cohort analysis), Hubspot's SaaS benchmark study, Reforge's SaaS metrics course.
