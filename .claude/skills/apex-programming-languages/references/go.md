# Go

## Scope
Idiomatic Go: simplicity, goroutines, interfaces, and the standard library.

## Core principles
- Errors are values: handle or return with wrapped context (`fmt.Errorf("op: %w", err)`); no exceptions.
- Accept interfaces, return structs; define interfaces where they're consumed, keep them small (1-3 methods).
- Share memory by communicating: channels and single-owner goroutines over mutex sprawl.
- Zero values should be useful; design structs so `var x T` works.
- gofmt is law; idiomatic Go looks the same everywhere — boring is the feature.

## Apex practices
- `context.Context` as first parameter through every blocking/IO call chain; honor cancellation.
- Table-driven tests with subtests; `go test -race` in CI always.
- Bound goroutines (errgroup, worker pools); every `go func()` needs an answer for "how does it stop?"
- Profile with pprof; check escape analysis before assuming allocations.

## Pitfalls
- Goroutine leaks from channels nobody reads/writes anymore.
- nil interface vs nil pointer inside interface — the `!= nil` check that lies.
- Copying sync types (mutex, WaitGroup) by value.

## Tools & references
Effective Go, golangci-lint, pprof, errgroup; "100 Go Mistakes" (Harsanyi).
