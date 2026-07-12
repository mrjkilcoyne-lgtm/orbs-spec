# LLM Observability

## Scope
Instrumenting LLM applications in production: tracing, logging, cost/latency/quality monitoring, feedback capture, and the analyze-iterate loop on real traffic.

## Core principles
- The trace is the unit of truth: for every request capture the full causal chain — rendered prompt (post-template), model+version+params, retrieved chunks, each tool call and result, raw completion, token counts, latency per span — because "what exactly did the model see?" is the first question in every incident and unanswerable without it.
- LLM systems degrade without deploys: provider model updates, drifting user behavior, and corpus growth shift quality while your code stays frozen — monitoring must therefore watch outputs (refusal rate, length, format-failure rate, eval scores on sampled traffic), not just uptime.
- Quality signals must be manufactured, because users rarely rate: instrument implicit feedback — regeneration clicks, copy events, edit distance between draft and what the user actually kept, conversation abandonment, human-handoff rate — these are your continuous quality metric.
- Cost and latency are per-feature dimensions, not one dashboard number: tag every call with feature/tenant/prompt-version so you can answer "which feature's tokens tripled this week?"; watch TTFT and P95/P99 (tail latency is where token-length variance lives), plus cache-hit rate as a first-class metric.
- Logged prompts and completions are user data: PII flows through them, so observability stores need the same retention, redaction, and access controls as the primary datastore — the trace store is a favorite target in LLM-app breaches.

## Apex practices
- Adopt OpenTelemetry GenAI semantic conventions (or a tool that emits them) so LLM spans nest inside your existing distributed traces — a slow answer might be the vector DB, not the model, and only unified tracing shows that.
- Close the flywheel: sample production traces weekly, review failures by hand, label them, and promote them into the eval suite — observability that doesn't feed evals is a very expensive log file.
- Version prompts, chains, and configs as first-class metadata on every trace, and diff quality metrics across versions — without prompt-version tags, A/B analysis and rollback attribution are guesswork.
- Alert on leading indicators with baselines: spike in format-parse failures, refusal rate, zero-retrieval-result rate, or output-length collapse often precedes user complaints by hours; static thresholds on token counts catch runaway agent loops before the invoice does.

## Pitfalls
- Logging only your own metadata and discarding raw prompts/completions — when a customer reports a bad answer, you have a status code and no way to reproduce.
- Averages hiding everything: mean latency and mean score look flat while P99 latency doubles and one tenant's quality craters; slice by percentile, tenant, and intent.
- Evaluating quality only pre-deploy: offline evals sample yesterday's distribution; without online scoring of sampled live traffic, drift is invisible until churn.

## Tools & references
Langfuse, LangSmith, Braintrust, Helicone, Arize Phoenix, OpenTelemetry GenAI semantic conventions, W&B Weave; pair with promptfoo/evals for the offline half of the loop.
