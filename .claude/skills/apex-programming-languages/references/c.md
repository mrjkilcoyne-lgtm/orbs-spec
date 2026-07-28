# C

## Scope
Portable systems C: memory discipline, undefined behavior, the toolchain.

## Core principles
- Undefined behavior is not "implementation quirk" — the optimizer assumes it never happens and will surprise you (signed overflow, OOB, strict aliasing).
- Every allocation has exactly one owner and one free path; design ownership before writing malloc.
- Arrays decay to pointers; sizes travel separately — pass (ptr, len) pairs religiously.
- The standard library string functions are footguns; know the safe variants and their still-sharp edges (strncpy's non-termination).
- Headers are the interface: minimal includes, include guards, opaque structs for encapsulation.

## Apex practices
- Compile with `-Wall -Wextra -Werror`; run ASan/UBSan/MSan in tests, Valgrind when sanitizers can't.
- Centralize cleanup with `goto err` unwind patterns — the idiomatic C answer to RAII.
- Use static analysis (clang-tidy, cppcheck) and fuzzing (libFuzzer/AFL) on every parser/decoder.
- Prefer fixed-width types (`uint32_t`), check every return value, and treat integer conversions as reviews-required.

## Pitfalls
- Off-by-one in buffer sizes (the `\0` byte) — the eternal CVE.
- Use-after-free from unclear ownership across module boundaries.
- Assuming struct layout/endianness for wire formats instead of explicit serialization.

## Tools & references
C11/C17 standard, sanitizers, Valgrind, "Modern C" (Gustedt), CERT C guidelines.
