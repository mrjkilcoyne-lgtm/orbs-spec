# Performance Testing

## Scope
Profiling applications to find bottlenecks: CPU time, memory allocation, I/O latency, and optimization opportunities.

## Core principles
- Performance bottlenecks are unintuitive; developers often optimize the wrong thing (algorithmic complexity that's 1% of runtime instead of I/O that's 80%).
- Flamegraphs (stack trace distributions) show where CPU time is spent; they're the primary tool for CPU profiling.
- Memory profiling (allocation tracking) finds excessive garbage collection or memory leaks; a 10GB heap that should be 1GB is a performance problem.
- Profiling must be representative: laboratory profiling (microbenchmarks) misses cache effects and memory pressure; production-like profiling is more useful.
- P99 latency is often driven by rare pathways (cache misses, GC pauses, lock contention) that don't show up in average case; test the tail.

## Apex practices
- Use production profilers (Pyroscope, Datadog, New Relic) to understand real workloads; laboratory environments have different cache and memory patterns.
- Profile before and after optimization to measure impact; a 10% optimization in a 1% bottleneck is wasted effort.
- Find the constraint (CPU, memory, I/O) and optimize that first; optimizing memory when you're CPU-bound helps nothing.
- Use timers and benchmarks: "for loop is O(n)" is not actionable, "loop takes 80% of requests' CPU" is.

## Pitfalls
- Micro-optimizing string handling when the bottleneck is database queries (wrong layer).
- Profiling in dev environment; CPU cache behavior and memory pressure are different in prod.
- Optimizing for the average case and ignoring tail latency (p99 matters for user experience).

## Tools & references
Pyroscope (continuous profiling), Datadog profiler, pprof (Go profiling), py-spy (Python), flamegraph.pl (visualization), async-profiler (Java), Speedscope (flamegraph viewer), perf (Linux CPU profiling).
