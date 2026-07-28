# Agents

## Scope
LLM systems that plan, call tools, observe results, and iterate in a loop toward a goal: agent loops, planning, memory, and stopping criteria.

## Core principles
- An agent is a model in a while-loop with tools and state; reliability comes from the loop's engineering (tool contracts, error feedback, termination) far more than from the model's cleverness.
- Errors compound geometrically: a step with 95% success yields ~60% over ten steps — so shorten trajectories, make individual steps trivially verifiable, and design tools that make illegal states unrepresentable.
- Give the agent the same feedback a human gets: raw stderr, HTTP bodies, diff output. Agents recover well from errors they can see and hallucinate around errors they can't.
- Bound everything: max iterations, per-tool timeouts, token/cost budgets, and an explicit escalate-to-human path — an unbounded agent loop is an unbounded bill and an unbounded blast radius.
- Prefer workflows over agents where the path is known (Anthropic's "Building Effective Agents"): a fixed prompt-chain or router is cheaper, faster, and more debuggable; reserve open-ended agency for genuinely open-ended tasks.

## Apex practices
- Make plans explicit artifacts: have the agent write a plan/todo list, execute against it, and re-plan on failure — visible plans are steerable and debuggable, latent ones aren't.
- Checkpoint state outside the context window (files, scratchpad, DB) so long tasks survive context compaction and crashes; context is working memory, not storage.
- Score agents on final task outcomes with an eval harness of real end-to-end tasks (SWE-bench-style: does the test pass? did the ticket resolve?), not on per-step plausibility.
- Gate irreversible actions (payments, deletes, sends, deploys) behind human approval or dry-run-first policies; classify every tool as read/write/irreversible and treat the classes differently.

## Pitfalls
- The 40-tool agent: tool-selection accuracy degrades as the toolbox grows; curate a minimal set per task or route to specialized sub-toolkits.
- Retrying a failed step with the identical context and expecting a different result — inject the failure, a hint, or an alternative strategy, or the agent loops on the same wall.
- Demo-driven confidence: agents look magical on the happy path and fall apart on distribution shift; the gap between a demo and a P95-reliable product is nearly all of the work.

## Tools & references
Anthropic "Building Effective Agents" (2024), ReAct (Yao et al. 2022), Claude Agent SDK, OpenAI Agents SDK, LangGraph, SWE-bench / GAIA / WebArena for benchmarks.
