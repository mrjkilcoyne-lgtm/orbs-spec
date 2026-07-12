# Cost & Latency Optimization

## Scope
Engineering LLM systems to be fast and affordable: model routing, caching, token dieting, batching, and the cost/latency/quality trade-off frontier.

## Core principles
- The unit economics are (input tokens × input price) + (output tokens × output price) per request, times requests — and output tokens are typically 3-5x the input price and dominate latency, so the highest-leverage instruction is often "be concise."
- Latency decomposes into TTFT (time to first token — driven by prompt length, prefill, and queueing) and TPOT (per-token generation); streaming hides TPOT from perceived latency, but nothing hides TTFT except shorter prompts, caching, and faster models.
- Prompt caching changes the architecture: cached prefix tokens cost 5-10x less and cut TTFT dramatically, but only if prompts are prefix-stable — put static content first and never interleave volatile data (timestamps, user IDs) into the shared prefix.
- Right-size the model per task: a router that sends 80% of traffic to a small model and escalates the hard 20% (by classifier, confidence, or user action) typically cuts cost 5-10x at near-flagship quality — one-model-for-everything is a budget decision made by default.
- Measure quality-per-dollar, not quality: the eval suite must run against every candidate model/config so the frontier (quality vs. cost vs. P95 latency) is a chart, not a debate.

## Apex practices
- Put a token diet on both ends: trim retrieved chunks to what's relevant, cap output with instructions plus max_tokens, and strip boilerplate from few-shot examples — 30-50% token reductions with zero quality loss are routine findings in a first audit.
- Use batch APIs (typically 50% discount) for anything async — evals, backfills, enrichment, digests; reserving realtime inference for realtime UX is often the single biggest bill cut.
- Exploit semantic/response caching for repeated questions with an explicit TTL and invalidation story, and cache at every deterministic layer (embeddings, retrieval, tool results) unconditionally.
- Set per-feature budgets and alerts (tokens/request, $/user/day) before launch; runaway agent loops and prompt regressions show up in the bill days before anyone notices in the product.

## Pitfalls
- Optimizing the model call while ignoring the pipeline: three sequential LLM calls plus two retrieval hops is a latency problem no faster model fixes — parallelize, fuse calls, or precompute.
- Breaking the prompt cache accidentally — a dynamic timestamp or reshuffled tool order at position zero silently multiplies input cost; monitor cache-hit rate as a first-class metric.
- Downgrading models on gut feel to save money, then quietly losing users to quality regression — every routing change goes through the eval suite and a canary.

## Tools & references
Provider pricing and prompt-caching docs, batch APIs (OpenAI/Anthropic), OpenRouter/LiteLLM for routing, vLLM (continuous batching, self-hosted), LLM observability cost dashboards (Langfuse, Helicone).
