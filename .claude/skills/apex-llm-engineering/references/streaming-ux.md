# Streaming UX

## Scope
Delivering LLM output progressively to users: SSE/WebSocket transport, rendering partial content, streaming with tools and structured data, and perceived-latency design.

## Core principles
- Perceived latency is TTFT, not total time: users tolerate a 20-second answer that starts in 300ms far better than a 6-second spinner — streaming is primarily a psychology optimization, and TTFT is its KPI.
- The transport is a long-lived HTTP response and everything in the path must cooperate: SSE requires disabling proxy buffering (nginx `X-Accel-Buffering: no`), heartbeats to survive idle timeouts, and awareness that serverless platforms may buffer or cap response duration.
- Partial output is invalid output: mid-stream markdown has unclosed fences and half-tables, mid-stream JSON doesn't parse — render with a streaming-tolerant parser and never hand incomplete structures to downstream logic.
- Streams fail mid-flight as a normal case, not an exception: design for disconnects with resumability (event IDs + reconnect cursor) or at minimum a clean "generation interrupted — retry" state; the last event must be an explicit done/error signal, never silence.
- Moderation and streaming are in tension: tokens shown cannot be unshown — run input-side checks before streaming, stream through an incremental output filter for high-risk surfaces, and design the retraction UX (replace with notice) for the rare post-hoc block.

## Apex practices
- Stream through your backend, never the provider key to the browser; the relay layer is also where you log usage, enforce quotas, and fan out to observability without adding TTFT.
- Handle the full event grammar, not just text deltas: tool-call events, thinking/reasoning deltas, usage reports, and stop reasons — UIs that only handle `content_delta` break the day tools are enabled.
- For structured streaming, stream fields progressively with a partial-JSON parser (render `title` as soon as it closes) or stream a human-readable channel while the structured payload arrives at the end.
- Smooth the visual cadence: buffer tokens slightly and render at a steady pace with auto-scroll that yields to user scroll — raw token jitter reads as glitchy, and hijacked scroll is the most-reported streaming annoyance.

## Pitfalls
- Testing only on localhost: production adds CDNs, proxies, and corporate middleboxes that buffer SSE — the classic symptom is "streaming works in dev, arrives all-at-once in prod."
- Counting tokens/cost from accumulated deltas instead of the stream's final usage event, then wondering why billing disagrees.
- Streaming everything reflexively: for sub-second short outputs (classifications, autocomplete), non-streaming is simpler and indistinguishable — streaming complexity should be paid only where generation is long.

## Tools & references
SSE spec (WHATWG), provider streaming APIs (Anthropic/OpenAI event formats), Vercel AI SDK, partial-json parsers, nginx/ALB idle-timeout and buffering docs.
