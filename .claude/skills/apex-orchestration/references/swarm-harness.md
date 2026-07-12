# Swarm Harness

## Scope
Running batched multi-agent execution: decomposition, spec-sharing, model-tiering, checkpointed waves, and the token economy that makes a throng cheaper than a soloist.

## Core principles
- Parallelize only what is independent: units that touch the same files, decisions, or state are ONE unit — merge conflicts and contradictory choices cost more than parallelism saves. The decomposition is the design; the launching is clerical.
- The spec is written once, referenced N times: a shared spec file (format, quality bar, exemplar pointers, rules) turns each agent prompt into a few lines — the single highest-leverage token optimization in multi-agent work, and it also makes quality uniform because every agent reads the same law.
- Tier the models to the work: bulk generation against a strong spec + exemplar goes to small/fast models (30x cheaper); taste-critical, ambiguous, or integrative work stays on the strong model; the exemplar the small models imitate is written by the strong model. Quality lives in the spec and exemplar, not in per-unit model size.
- Waves with checkpoints, not one big bang: launch a batch → verify mechanically (file counts, format greps, spot-reads) → commit → next wave. A checkpoint converts a failed wave into a bounded loss and a committed wave into progress that survives session death, rate limits, and container reclaim — plan for the harness itself to fail (limits, disconnects) because it does.
- One writer owns integration: subagents never run git, never edit shared indexes, never touch each other's paths; the orchestrator commits, resolves, and reports. Cheap agents + strict boundaries beats smart agents + shared mutable everything (the single-writer principle from concurrency, applied to organizations).

## Apex practices
- Resumable-by-design prompts: every agent instruction says "check what exists, write only what's missing" — waves become idempotent, and a killed wave restarts for the cost of an ls.
- Verify outputs mechanically before trusting reports: agents' self-reports are claims; `ls | wc -l`, format greps, and one random deep-read per agent are the evidence (verification-before-assertion applies doubly to delegated work).
- Budget before launching: units × tokens-per-unit × model-tier, compared against the inline alternative — below ~5 independent units the swarm's fixed costs (spec, launch, verification, integration) rarely pay.
- Keep agent prompts to: spec pointer + assignment list + deviation-reporting instruction. Everything else is duplication the spec already covers.

## Pitfalls
- The 99%-parallel trap: parallelizing generation but serializing through one unspecified decision ("agents, choose a consistent style") — anything needing consistency goes in the spec or doesn't go to the swarm.
- Trusting completion summaries without mechanical verification — a confident "all 20 files written" from an agent that wrote 17.
- Re-sending full context per agent instead of a spec file; ten agents × full context = the token bill that motivated this doctrine.

## Tools & references
Claude Code Agent tool (background waves, model tiering), shared spec files in scratchpad, git checkpoint commits, this repo's build (500 areas, 2 waves, 7+3 agents) as the worked example.
