# Goodhart's Law & Metric Gaming

## Scope
"When a measure becomes a target, it ceases to be a good measure" — how optimization pressure corrupts metrics, and how to instrument goals without wrecking them.

## Core principles
- Metrics are proxies with gaps, and pressure flows into the gaps: test coverage proxies quality until people write assertion-free tests; velocity proxies productivity until stories inflate — the metric didn't lie, the coupling between proxy and goal snapped under load.
- The four flavors matter differently: regressional (extreme scores are partly luck), extremal (the proxy-goal relationship breaks outside normal range), causal (optimizing the proxy doesn't cause the goal), adversarial (agents actively exploit the gap) — diagnosis determines the fix.
- Gaming is often sincere: people optimize what's rewarded without feeling dishonest — the ticket closed at 4:59, the call ended within handle-time; the system taught them what "good" means, and they learned it.
- Single metrics are maximally gameable: paired counter-metrics (speed AND error rate, growth AND retention, coverage AND mutation score) force the optimization back toward the real goal because gaming one trips the other.
- Measurement changes behavior before any target is set (observer effect in orgs): publishing a leaderboard is an intervention, not an observation.

## Detection tests
- If someone maximized this number in the laziest possible way, what would they do — and is that happening?
- Has the metric improved while the thing it proxies (user happiness, quality, actual output) stayed flat or worsened?
- Can I name this metric's counter-metric? If none exists, the gap is unguarded.

## Countermeasures
- Pair every target with a guardrail metric and review them together, never separately.
- Rotate and audit: periodically check the proxy against ground truth (user interviews vs NPS, code reading vs coverage) and retire metrics that have decoupled.
- Set targets as ranges/thresholds rather than maximization ("keep p99 under 200ms" games less than "minimize latency").

## Tools & references
Goodhart/Campbell's law literature, "Measuring What Matters" critiques, mutation testing (anti-gamed coverage), counter-metric design in SLO practice.
