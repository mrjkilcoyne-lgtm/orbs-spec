# Product Metrics

## Scope
Choosing and structuring the metrics that describe product health: north star design, metric trees, input vs. output metrics, and guardrails.

## Core principles
- A north star metric must capture value delivered to customers, not value extracted from them: Airbnb's nights booked and Spotify's time listening work because a customer who drives the metric up got something; revenue is a lagging receipt, not a north star.
- Decompose the north star into a metric tree of input metrics teams can actually move (north star = f(acquisition, activation, frequency, depth)); teams own inputs, leadership watches the output — assigning a team the output alone produces dashboard-staring, not action.
- Distinguish leading from lagging: churn is a lagging autopsy; declining usage frequency 6 weeks prior is the leading symptom you can still act on. Every lagging KPI needs a named leading proxy.
- Ratio and cohort metrics beat cumulative vanity: "total registered users" only goes up; DAU/MAU, week-4 retention by signup cohort, and activation rate can go down, which is exactly what makes them informative.
- Goodhart's law is a design constraint, not trivia: any metric under pressure gets gamed, so pair each target metric with a counter-metric (speed with quality, engagement with "regrettable" usage flags) at design time.

## Apex practices
- Define every metric in a metrics dictionary with owner, exact SQL/event definition, and known caveats; "activation" meaning three different queries in three dashboards is how orgs argue about facts.
- Instrument the HEART framework (Happiness, Engagement, Adoption, Retention, Task success — Google) for feature-level health instead of inventing per-feature vanity counters.
- Segment before celebrating or panicking: a flat aggregate often hides a growing segment offset by a dying one (Simpson's paradox appears constantly in mixed cohorts).
- Review metrics weekly at fixed altitude — team reviews inputs, leadership reviews the tree — and re-derive the tree annually as the product's value model shifts.

## Pitfalls
- Vanity metrics as headline numbers: cumulative signups, page views, and app downloads that can't decrease and correlate with nothing.
- Averages hiding distributions: "average session 8 minutes" from a bimodal blob of 30-second bounces and 40-minute power users prescribes the wrong action for both.
- Shipping features with no success metric declared beforehand, then retro-fitting whichever chart went up ("HARKing" for product).

## Tools & references
Amplitude's North Star Playbook, Google HEART framework, AARRR (Dave McClure), Croll & Yoskovitz "Lean Analytics," metric-tree practice from Reforge.
