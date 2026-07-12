# TypeScript

## Scope
TypeScript's structural type system as a design tool over JavaScript.

## Core principles
- Structural typing: shape compatibility, not name; two identical interfaces are interchangeable.
- Types are erased at runtime — validation at boundaries (zod & co.) is still required for external data.
- Discriminated unions + exhaustive `switch` (with `never` check) encode state machines the compiler enforces.
- `any` is an off-switch that spreads; `unknown` is the safe top type that forces narrowing.
- Type inference is strongest with `const`, literal types, and return-type inference — annotate boundaries, infer internals.

## Apex practices
- `strict: true` always; add `noUncheckedIndexedAccess` for honesty about arrays/records.
- Model states, not flags: `{status:'loading'} | {status:'error'; error} | {status:'ok'; data}` beats three booleans.
- Derive types from single sources of truth (`typeof`, `keyof`, `ReturnType`, schema inference) instead of duplicating.
- Keep clever generic gymnastics in library code; application code should read plainly.

## Pitfalls
- Type assertions (`as`) papering over real mismatches — they're unchecked promises.
- Enums vs unions confusion; string literal unions are usually the better fit.
- Trusting types on `JSON.parse`/API responses without runtime validation.

## Tools & references
tsconfig strictness flags, zod/valibot, ts-reset, "Effective TypeScript" (Vanderkam).
