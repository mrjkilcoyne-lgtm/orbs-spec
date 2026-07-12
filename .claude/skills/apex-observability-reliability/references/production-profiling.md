# Production Profiling

## Scope
Continuous profiling in production: understanding real workload, identifying performance regressions, and detecting resource leaks.

## Core principles
- Production profiling captures the real workload (cache behavior, memory pressure, traffic patterns) that lab profiling misses.
- Overhead must be minimal (< 5% CPU) to avoid amplifying the problem you're investigating; sample-based profiling (pprof, Pyroscope) is lower-overhead than instrumentation.
- Continuous profiling (always on, low overhead) enables historical analysis: was performance always this bad, or did a recent change degrade it?
- Flamegraphs from production often reveal surprising bottlenecks (unexpected hot codepaths, inefficient library calls) that never appeared in testing.
- Heap profiling detects memory leaks (growing allocated objects) and excessive allocation (allocator churn, GC pressure).

## Apex practices
- Enable continuous profiling (Pyroscope) on production services; the overhead is negligible and the insights are invaluable.
- Profile at a per-endpoint granularity; you can't optimize "requests" globally, but you can optimize "GET /search" specifically.
- Compare profiles before and after deployments to detect regressions early (not in production for a week).
- Set up alerts for profile anomalies: if the top function in a profile changes, that might indicate a regression.

## Pitfalls
- Profiling only when there's a problem; continuous profiling establishes a baseline and detects regressions.
- Profiling overhead that skews results; a profiler that adds 50% overhead is unreliable.
- Profiling without action; profiling data is only useful if you're actually optimizing based on it.

## Tools & references
Pyroscope (continuous profiling, CNCF), Datadog profiler, New Relic, pprof (Go), py-spy (Python), async-profiler (Java), flamegraph.pl, profile-guided optimization (PGO), memory profiling (valgrind, heaptrack).
