# Estimation

## Scope
Forecasting software effort and delivery dates: techniques, uncertainty communication, and the politics of numbers.

## Core principles
- The planning fallacy (Kahneman & Tversky) is systematic, not random: humans estimate the best-case path and forget integration, review, rework, and interrupts — which is why "reference-class forecasting" (what did similar work actually take?) beats introspection.
- Estimates are probability distributions, not points: the honest answer is "50% chance by March 10, 85% by April 2," and any process that forces a single date silently picks an unstated percentile — usually the 20th.
- The cone of uncertainty is real but asymmetric: software estimates miss long far more often than short, because scope grows and unknowns are discovered, never un-discovered.
- An estimate, a target, and a commitment are three different things (McConnell); most estimation dysfunction is a target ("the conference is June 5") being laundered into an "estimate" after the fact.
- Estimation accuracy improves more by shrinking the work than by improving the guessing: a 2-day task's error is bounded; a 2-month epic's error is a career event.

## Apex practices
- Forecast from throughput data with Monte Carlo simulation (sample historical weekly completions, run 10,000 trials, report the 85th percentile) — it's less effort than planning poker and more accurate.
- Decompose until no item exceeds a few days, then count items instead of summing hour-estimates; count-based forecasts are robust to individual-item error.
- Communicate dates as ranges with confidence levels and update them weekly as data arrives; a silently slipping date destroys more trust than a wide honest range ever will.
- Record estimates vs. actuals and review the ratio quarterly — most teams discover a stable 1.5-2.5x multiplier they can simply apply.

## Pitfalls
- Negotiating the estimate instead of the scope ("can you make it 3 weeks?" changes the number, not the work) — anchoring pressure produces compliant fiction.
- Summing best-case task estimates and presenting the total at ~50 tasks; independent optimistic errors don't cancel, they compound with correlated omissions.
- Padding secretly instead of stating uncertainty openly; hidden buffers get discovered, trust collapses, and the next cycle they're stripped (Parkinson's law eats them anyway).

## Tools & references
McConnell "Software Estimation: Demystifying the Black Art," Kahneman "Thinking, Fast and Slow" (planning fallacy), Flyvbjerg's reference-class forecasting work, Vacanti's Monte Carlo throughput forecasting, #NoEstimates debate for the counterpoint.
