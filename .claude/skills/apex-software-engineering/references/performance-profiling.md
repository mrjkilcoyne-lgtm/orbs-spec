# Performance & Profiling

## Scope
Measuring where time and memory go, and optimizing with evidence.

## Core principles
- Measure before optimizing; intuition about hot spots is wrong more often than right.
- Optimize the workload you actually serve — profile production-shaped inputs.
- Big-O dominates constants at scale; algorithm and data-structure choice first, micro-tuning last.
- Latency and throughput trade off; know which one the requirement names, and which percentile (p50 vs p99).
- Every optimization has a complexity cost; keep the unoptimized version's clarity when the win is small.

## Apex practices
- Use CPU/alloc profilers (pprof, perf, flame graphs) and read the widest frames, not the deepest.
- Benchmark with statistical rigor: warmup, multiple runs, variance reported; beware dead-code elimination.
- Set budgets (latency SLO, memory ceiling) so "fast enough" is defined before you start.
- Fix the biggest bottleneck, re-measure, repeat — bottlenecks move.

## Pitfalls
- Optimizing code that accounts for 2% of runtime.
- Microbenchmarks that measure the benchmark harness.
- Caching as a first resort, introducing staleness bugs to avoid measuring.

## Tools & references
perf, pprof, flamegraphs (Brendan Gregg), hyperfine, "Systems Performance" (Gregg).
