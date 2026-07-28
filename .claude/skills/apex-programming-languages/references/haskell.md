# Haskell

## Scope
Pure functional programming: laziness, the type system, monadic effects.

## Core principles
- Purity means effects live in types: IO for the outside world, and the type signature tells the truth about a function.
- Laziness is default: enables elegant infinite structures and equational reasoning, but space leaks come from unforced thunks.
- Algebraic data types + exhaustive pattern matching: model the domain first, functions follow.
- Type classes are principled overloading (Functor→Applicative→Monad hierarchy); laws matter, not just shapes.
- Parametricity works for you: a function `a -> a` can only be identity — general types constrain implementations.

## Apex practices
- Design with total functions; make partiality explicit (Maybe/Either) and banish `head`/`fromJust`.
- Use `newtype` liberally for domain distinction (UserId vs Text) at zero cost.
- Force strictness deliberately: strict fields (bang patterns), `foldl'`, profiling for space leaks (+RTS -h).
- Keep the effect stack simple (ReaderT pattern over IO beats a five-layer transformer tower for apps).

## Pitfalls
- String (linked list of Char) in performance paths — use Text/ByteString.
- Space leaks from lazy accumulation in folds/state.
- Type-class-astronautics: needing a PhD to add a field.

## Tools & references
GHC + HLS, "Haskell Programming from First Principles", hlint, "Production Haskell" (Parsons).
