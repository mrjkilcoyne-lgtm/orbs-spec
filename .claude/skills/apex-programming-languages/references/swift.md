# Swift

## Scope
Swift for Apple platforms and server: value types, optionals, protocols, ARC.

## Core principles
- Value semantics first: structs and enums with copy-on-write; classes only for identity/reference needs.
- Optionals are the null-safety system: `if let`/`guard let` unwrapping, `??` defaults; `!` is a crash you scheduled.
- Protocol-oriented design: protocols + extensions + generics over class hierarchies.
- ARC means retain cycles are your job: `[weak self]` in escaping closures that capture self.
- Swift concurrency (async/await, actors) replaces callback pyramids; actors serialize access to mutable state.

## Apex practices
- `guard` for early exit keeps the happy path unindented.
- Exhaustive `switch` over enums; add cases and let the compiler find every site.
- Use `Codable` for serialization boundaries with explicit CodingKeys when the wire format differs.
- Mark Sendable conformance honestly; data races are compile-time errors in strict concurrency — embrace it.

## Pitfalls
- Massive view controllers / god ViewModels — Swift makes small value types cheap, use them.
- Force-unwrapping IBOutlets/JSON paths in production code.
- Ignoring main-actor isolation and touching UI off the main thread.

## Tools & references
Swift.org book, SwiftLint, Instruments, swift-format; WWDC session library.
