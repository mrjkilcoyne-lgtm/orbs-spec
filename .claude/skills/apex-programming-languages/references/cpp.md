# C++

## Scope
Modern C++ (17/20/23): RAII, move semantics, templates, the subset worth using.

## Core principles
- RAII is the language's soul: every resource in an object whose destructor releases it; if you write `delete`, you've usually already lost.
- Rule of zero: let smart pointers and containers manage lifetime; write the five special members only in resource-owning classes.
- Move semantics make ownership transfer explicit and cheap; understand what `std::move` does (a cast, not a move).
- The type system is your prover: `const` everywhere possible, `enum class`, `std::variant`/`optional` over unions and sentinels.
- C++ is a federation of languages — pick and enforce your project's subset (Core Guidelines).

## Apex practices
- `unique_ptr` by default, `shared_ptr` only for genuinely shared lifetime; raw pointers as non-owning observers.
- Sanitizers + `-Wall -Wextra` + clang-tidy in CI; templates checked with concepts (C++20) for readable errors.
- Prefer algorithms/ranges over raw loops; prefer `std::span`/`string_view` for non-owning views (mind lifetimes).
- Keep compile-time metaprogramming behind clean interfaces; error novels are a tax on the whole team.

## Pitfalls
- Dangling `string_view`/`span`/references to temporaries — lifetime bugs the compiler mostly won't catch.
- Object slicing when passing derived by value.
- Undefined behavior via iterator invalidation during container mutation.

## Tools & references
C++ Core Guidelines, cppreference.com, clang-tidy, Compiler Explorer, "Effective Modern C++" (Meyers).
