# Multi-Agent Systems

## Scope
Systems composed of multiple LLM agents: orchestrator-worker patterns, sub-agent delegation, inter-agent communication, and deciding when multiple agents beat one.

## Core principles
- Multi-agent is a context-management strategy before it's anything else: the legitimate win is isolation — a sub-agent burns 100k tokens exploring and returns a 500-token answer, keeping the orchestrator's context clean; if you're not buying isolation or parallelism, one agent is better.
- Every agent boundary is a lossy channel: sub-agents don't share the parent's context, so the task brief must be written like a spec for a contractor — goal, constraints, output format, and what's already known; vague delegation returns confident irrelevance.
- Orchestrator-worker with results funneling back to one decision-maker is the pattern that works in practice; free-form peer-to-peer agent "societies" demo well and drift into unrecoverable miscommunication — keep the topology a tree, not a mesh.
- Errors and costs multiply across agents: N agents each 90% reliable, chained, yield 0.9^N system reliability, and token spend scales with agent count (Anthropic measured ~15x a single chat's tokens for research tasks) — every added agent must pay for itself on the eval.
- Parallelism only helps decomposable work: fan out for independent subtasks (search five sources, review ten files), never for sequentially dependent reasoning — parallel agents writing to shared state without coordination produce merge conflicts in prose.

## Apex practices
- Give the orchestrator explicit delegation heuristics in its prompt: when to spawn, how many, how to size a task brief, and what a sufficient result looks like — undirected orchestrators either never delegate or spawn swarms for trivia.
- Specialize workers by role with tailored prompts and minimal toolsets (researcher: search+read; coder: edit+test) rather than cloning generalists; narrower agents are more reliable and cheaper to eval.
- Make hand-offs structured artifacts (JSON briefs, files, shared scratchpads with defined schemas), not chat transcripts — downstream agents shouldn't parse upstream small talk.
- Trace the whole tree: every sub-agent's context, cost, and result linked to its parent span, because "which agent went wrong and what did it actually see?" is the debugging question you'll ask daily.

## Pitfalls
- Multi-agent as cargo cult: splitting a task one strong model with good tools handles into five agents adds latency, cost, and failure modes while lowering quality — always benchmark against the single-agent baseline.
- Telephone-game degradation: each summarize-and-forward hop drops constraints; by hop three, the worker is solving a subtly different problem than the user posed.
- Unbounded recursive spawning (agents spawning agents) without depth/budget caps — the distributed-systems equivalent of a fork bomb, billed per token.

## Tools & references
Anthropic "How we built our multi-agent research system" (2025), Claude Agent SDK subagents, LangGraph, OpenAI Agents SDK handoffs, AutoGen/CrewAI (patterns; verify against single-agent baselines).
