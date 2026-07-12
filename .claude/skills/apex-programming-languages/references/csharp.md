# C#

## Scope
Modern C# on .NET: async/await, LINQ, records, the runtime.

## Core principles
- async/await all the way down: blocking on async (`.Result`, `.Wait()`) invites deadlocks and starves the thread pool.
- LINQ is lazy: queries execute on enumeration; multiple enumeration repeats work and side effects.
- Records + init-only + pattern matching support immutable domain modeling; classes remain for identity/behavior.
- Nullable reference types on (`#nullable enable`) turn the billion-dollar mistake into warnings — keep them as errors.
- The runtime is observable and tunable: GC modes, Span<T>/Memory<T> for allocation-free hot paths.

## Apex practices
- `ConfigureAwait(false)` in libraries; CancellationToken parameters through every async chain.
- Dependency injection via the built-in container; options pattern for configuration.
- Use `IAsyncEnumerable` for streaming, channels for producer/consumer.
- Benchmark with BenchmarkDotNet; profile allocations before sprinkling Span.

## Pitfalls
- async void (uncatchable exceptions) anywhere but event handlers.
- Capturing loop variables/disposables in closures with deferred execution.
- Entity Framework queries that silently switch to client-side evaluation.

## Tools & references
.NET docs, BenchmarkDotNet, Roslyn analyzers, "C# in Depth" (Skeet).
