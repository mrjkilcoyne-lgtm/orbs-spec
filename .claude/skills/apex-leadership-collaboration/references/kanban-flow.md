# Kanban & Flow

## Scope
Managing knowledge work as a flow system: visualizing work, limiting WIP, and optimizing cycle time.

## Core principles
- Little's Law is the physics of the board: average cycle time = WIP / throughput — the only reliable way to ship faster without hiring is to start less; finishing is downstream of not-starting.
- WIP limits are the mechanism, not the goal: they convert "I'm blocked, I'll start something new" into "I'm blocked, let's swarm the blocker" — a full column is a conversation trigger.
- Flow efficiency (touch time / total cycle time) in most orgs is 5-15%: work spends most of its life waiting in queues and handoffs, so attacking wait states beats making people work faster by an order of magnitude.
- Variability kills predictability: right-size work items (split anything over ~2-3 days), and forecast probabilistically from cycle-time scatter ("85% of items finish within 9 days") instead of point estimates.
- Kanban is evolutionary: start with what you do now, visualize it honestly (including the hidden "waiting on security review" column), then improve — no reorg, no role changes, no big bang.

## Apex practices
- Track and review the cumulative flow diagram weekly: widening bands show where WIP accumulates, flat bands show starvation — the CFD is an X-ray of your process.
- Set explicit per-column policies ("done here means: reviewed + deployed to staging") so "done-ness" isn't renegotiated per ticket.
- Use classes of service (expedite, fixed-date, standard, intangible) with visible policies instead of letting every stakeholder claim their item is urgent.
- Measure item aging in-progress and swarm anything older than the 85th percentile — aging WIP is the earliest leading indicator of a blown forecast.

## Pitfalls
- A board with WIP limits nobody enforces — it's a status wallpaper, and Little's Law doesn't care about your columns' decoration.
- Optimizing resource utilization to 100%: queueing theory says wait times explode nonlinearly past ~80% utilization (M/M/1: wait ∝ ρ/(1−ρ)); busy-ness is the enemy of throughput.
- Per-person swimlanes, which quietly reinstate individual task assignment and kill swarming.

## Tools & references
Anderson "Kanban: Successful Evolutionary Change," Vacanti "Actionable Agile Metrics for Predictability," Reinertsen "The Principles of Product Development Flow," Little's Law (1961).
