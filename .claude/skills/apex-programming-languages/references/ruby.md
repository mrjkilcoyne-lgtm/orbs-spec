# Ruby

## Scope
Ruby's object model, metaprogramming, and the Rails-shaped ecosystem.

## Core principles
- Everything is an object and almost everything is a method call; blocks/procs/lambdas are the composition idiom.
- Duck typing with confidence: design to messages, not classes; respond_to? over is_a? checks.
- Metaprogramming (define_method, method_missing) is power for libraries, poison for application code readability.
- Convention over configuration: fighting Rails costs more than learning its grain.
- Optimize for programmer happiness means readability: code should read like intent.

## Apex practices
- Keep controllers thin, models focused; extract service/query objects when either bloats.
- Use frozen string literals, keyword arguments for clarity, and pattern matching (case/in) for structured data.
- Test with the community grain (RSpec/minitest, factories over fixtures, request specs over controller specs).
- Profile N+1 queries (bullet) — the classic Rails performance failure is in the ORM, not Ruby.

## Pitfalls
- Monkey-patching core classes in app code; surprises every future reader.
- Rescue-all (`rescue => e`) hiding real failures.
- Callback soup (before_save chains) encoding business logic invisibly.

## Tools & references
RuboCop, RSpec, Sorbet/RBS for gradual types, "Practical Object-Oriented Design" (Metz).
