# Zig

## Scope
Zig for systems programming: explicit allocation, comptime, C interop without a C compiler.

## Core principles
- No hidden control flow, no hidden allocation: every allocating function takes an allocator parameter — callers own policy.
- comptime replaces macros, generics, and codegen: ordinary Zig code executed at compile time.
- Errors are values in error sets; `try` propagates, `catch` handles, and `errdefer` unwinds partial work.
- Optionals (`?T`) and explicit casts kill entire bug classes; there is no null pointer surprise, only unwrapped intent.
- Zig is also a C toolchain: translate-c, cross-compilation out of the box, incremental adoption inside C codebases.

## Apex practices
- Pick allocators per context: GeneralPurposeAllocator (leak detection) in debug, arena for request/frame scopes.
- `defer`/`errdefer` immediately after acquisition — cleanup lives next to creation.
- Use slices (`[]T`) with explicit lengths everywhere; sentinel-terminated types only at C boundaries.
- Lean on the test blocks (`test {}` in-file) and `zig build test`; comptime asserts for invariants.

## Pitfalls
- Returning pointers to stack memory or arena memory that outlives the arena.
- Ignoring `error{OutOfMemory}` paths because "it won't happen."
- comptime golf that turns build errors into archaeology.

## Tools & references
ziglang.org docs + std source (readable!), zls, "Zig in 30 minutes" community guides, ziglearn.org.
