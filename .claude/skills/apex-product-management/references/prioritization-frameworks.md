# Prioritization Frameworks

## Scope
Deciding what to build next when demand exceeds capacity: scoring models, cost-of-delay thinking, and the judgment they support.

## Core principles
- All frameworks are value ÷ cost with different costumes: RICE (Reach × Impact × Confidence ÷ Effort), WSJF (Cost of Delay ÷ Duration), ICE — the arithmetic matters less than forcing explicit estimates that can be challenged.
- Cost of Delay is the master concept (Don Reinertsen, "The Principles of Product Development Flow"): prioritize by CD3 (cost-of-delay divided by duration), because a small item bleeding $50k/week beats a large item worth $1M someday.
- Confidence is the most-gamed input: RICE without evidence standards becomes "my number is bigger than yours"; tie confidence scores to evidence tiers (shipped experiment > user interviews > internal opinion).
- Kano analysis separates dimensions that scoring flattens: basic expectations (absence enrages, presence is invisible), performance features (linear), and delighters (nonlinear) — a backlog sorted purely by RICE systematically underfunds basics until churn spikes.
- Frameworks rank comparable items within a strategy; they cannot choose between strategies. Deciding "platform investment vs. growth features" is a portfolio allocation decision made first, then frameworks rank within each bucket.

## Apex practices
- Allocate capacity into buckets before scoring (e.g., 50% roadmap / 25% platform-debt / 15% KTLO / 10% bets) so infrastructure never has to out-RICE a shiny feature.
- Score in pairs or triads, not solo: divergent Reach estimates between PM and engineer are the highest-value conversation the framework produces.
- Re-score quarterly and audit last quarter's scores against actuals — teams that never check whether "Impact: 3" materialized never calibrate.
- Use opportunity scoring (importance vs. satisfaction gap, from ODI/Ulwick) on discovery inputs so the backlog reflects underserved needs, not just the loudest requests.

## Pitfalls
- Weighted-scoring theater: 11-factor spreadsheets whose weights were reverse-engineered to justify the pre-decided answer.
- Ignoring effort denominators from engineers ("that's a 2, right?") — a RICE score with a fabricated Effort is worse than no score.
- Treating stack rank as sacred for a quarter: cost of delay changes when a competitor ships or a deal-blocking gap emerges, and the rank must follow.

## Tools & references
Reinertsen "Principles of Product Development Flow" (WSJF/CD3), Intercom's RICE, Kano model, Ulwick "Jobs to Be Done"/ODI opportunity scores, ITAMar Gilad's ICE + confidence meter.
