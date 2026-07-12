# Rust

## Scope
Ownership-based systems programming: borrow checker, traits, fearless concurrency.

## Core principles
- Ownership: each value has one owner; moves transfer, borrows lend (&) exclusively-mutable (&mut) or shared-immutable.
- Fight the borrow checker with design, not clones: restructure who owns what before reaching for `Rc<RefCell<>>`.
- `Result`/`Option` with `?` make failure explicit; `unwrap` in production code is a documented decision or a bug.
- Traits are the abstraction unit; generics monomorphize (fast), `dyn Trait` boxes (flexible).
- Unsafe is a contract: encapsulate it in a module whose safe API upholds the invariants, document why.

## Apex practices
- Model with enums + exhaustive match; make invalid states unrepresentable.
- Use iterators and combinators — they compile to loop-equivalent code and encode intent.
- clippy pedantic as advisor, rustfmt as law; deny warnings in CI.
- Prefer borrowing in APIs (`&str`, `&[T]`) and owned types in storage (String, Vec).

## Pitfalls
- Cloning everywhere to silence the checker, then wondering about performance.
- Blocking calls inside async executors starving the runtime.
- Lifetime annotations added by trial-and-error instead of understanding whose data outlives whom.

## Tools & references
The Book, clippy, cargo ecosystem (serde, tokio, thiserror/anyhow); "Rust for Rustaceans" (Gjengset).
