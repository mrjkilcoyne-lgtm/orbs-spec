# Context Management

## Scope
Deciding what goes into the model's context window and when: context budgets, compaction, memory architectures, and long-conversation strategies.

## Core principles
- Context is a scarce, degrading resource: advertised windows (200k-1M tokens) are not free capacity — effective attention degrades with length ("context rot"), so the goal is the smallest set of high-signal tokens, not the fullest window.
- Position is signal: models attend best to the beginning and end of context; pin stable instructions at the top, put the live question at the bottom, and expect the middle to be skimmed (Liu et al., "Lost in the Middle").
- Separate working memory from storage: the window holds what's needed now; durable state (task lists, decisions, learned facts) belongs in files/DBs the model reads back on demand — an agent that "remembers" only via context forgets at the first compaction.
- Every token has a cost triple — money, latency, and attention dilution; a 50k-token context that could be 8k is a 6x cost increase and often a quality decrease.
- Compaction is lossy and must be engineered: summarize with a purpose-built prompt that preserves decisions, open questions, constraints, and file/ID references — a generic "summarize this" drops exactly the details the next step needs.

## Apex practices
- Set explicit token budgets per component (system prompt, tools, retrieved docs, history) and instrument them; when quality drops, the first diagnostic is "what was actually in context?"
- Use retrieval-on-demand over preloading: give agents search/read tools and let them pull what they need ("just-in-time context") instead of stuffing everything speculatively.
- Structure prompts for prefix-cache stability: static content first (system, tools, examples), volatile content last — reordering breaks prompt caching and multiplies cost.
- For long conversations, compact at natural boundaries (task completion, topic shift), keep the last N turns verbatim, and write durable facts to an external memory before dropping them from the window.

## Pitfalls
- The kitchen-sink context: dumping whole files, full API responses, and entire chat history "just in case" — needle-in-haystack scores mislead; real multi-fact reasoning degrades well before the window is full.
- Losing task-critical constraints in summarization (the user's "must be under $100" vanishes at turn 40) — compaction prompts need an explicit checklist of what to preserve.
- Treating context limits as an error path ("truncate whatever doesn't fit") instead of a designed policy of what to evict, in what order, with what preserved.

## Tools & references
"Lost in the Middle" (Liu et al. 2023), Anthropic "Effective context engineering for AI agents", provider prompt-caching docs, MemGPT/Letta (memory-hierarchy pattern), RULER long-context benchmark.
