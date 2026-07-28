# Cost Commitments & Reserved Instances

## Scope
Optimizing cloud spending through reservations and commitments: reserved instances, savings plans, commitment strategies, and trade-offs.

## Core principles
- Reserved instances (RIs) and savings plans lock you into a price for 1-3 years; use for predictable, baseload capacity only.
- Spot instances are up to 90% cheaper than on-demand but can be interrupted; use for fault-tolerant workloads (batch, stateless services with autoscaling).
- Commitment strategy depends on predictability: 100% on-demand if unpredictable, mix of RIs and on-demand if predictable, spot for high variance.
- Upfront payment (1-year or 3-year RIs) provides the best discount but ties up money and risk if requirements change.
- Regional RIs are less flexible (locked to a region and AZ) but cheaper; zonal RIs are regional (can move between AZs in a region) and slightly more expensive.

## Apex practices
- Analyze usage patterns: identify baseload (stable minimum) and peaks; reserve the baseload, use on-demand for peaks.
- Use savings plans for better flexibility than regional RIs (work across instance types and regions, automatically apply to most used services).
- Combine reserved instances with autoscaling: autoscale on-demand instances, use RIs for the stable baseline.
- Monitor reserved instance utilization; unused reservations are wasted money — buy only what you'll use.

## Pitfalls
- Buying 3-year commitments for rapidly-changing workloads (technology changes, requirements shift, you're locked in).
- Reservations without monitoring; you pay for capacity you don't use.
- Over-committing (reserved more capacity than you use) — buy conservatively, increase if you hit limits.

## Tools & references
AWS Cost Explorer, Compute Optimizer for rightsizing, AWS Reserved Instance reports, Infracost for savings plan recommendations, finops.org.
