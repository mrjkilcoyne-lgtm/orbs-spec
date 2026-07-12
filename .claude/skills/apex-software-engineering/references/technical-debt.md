# Technical Debt

## Scope
Recognizing, communicating, and strategically paying down expedient design decisions.

## Core principles
- Debt is a metaphor for leverage: deliberate shortcuts with known interest — not a synonym for "code I dislike."
- The interest rate is what matters: debt in code nobody changes costs nothing; debt on the hot path compounds daily.
- Distinguish quadrants (deliberate/inadvertent × prudent/reckless); each needs a different response.
- Debt is invisible to non-engineers until translated into slowed features and incident counts.
- Zero debt is the wrong target; unbounded debt is bankruptcy. Manage the portfolio.

## Apex practices
- Make it visible: a registry (issues tagged, ADR-style entries) with location, cost symptoms, and payoff estimate.
- Pay as you go: the boy-scout rule inside touched files, budgeted capacity (~10-20%) for larger items.
- Attach paydown to feature work in the same area — "we're in this code anyway" halves the cost.
- Re-evaluate periodically: some debt gets written off when the code is deleted.

## Pitfalls
- The "refactoring sprint" that gets cancelled every quarter — debt work must ride with normal delivery.
- Calling everything debt until the term means nothing to leadership.
- Paying down low-interest debt for comfort while the high-interest hotspot stays scary.

## Tools & references
Fowler's debt quadrant, hotspot analysis (code churn × complexity, e.g. CodeScene), issue-tracker debt registries.
