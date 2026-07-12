# Legacy Modernization

## Scope
Evolving valuable-but-aged systems: untested code, dead frameworks, big-ball-of-mud architectures.

## Core principles
- Legacy code is code without tests (Feathers); the first move is characterization tests that pin current behavior.
- The system's behavior — including its bugs — is the spec someone may depend on (Hyrum's Law).
- Strangler fig beats rewrite: new code fronts old, traffic shifts incrementally, old dies quietly.
- Understand before changing: the weird code usually encodes a forgotten requirement.
- Rewrites reset all learned edge cases to zero; they're justified rarely and must ship incrementally anyway.

## Apex practices
- Find seams (Feathers): places to inject tests without invasive change — wrap, subclass, link-time substitution.
- Put a facade in front, freeze the old interface, and modernize behind it.
- Migrate with parallel-run verification: both paths execute, diffs get logged, confidence accrues before cutover.
- Delete relentlessly once traffic proves code dead; dead code taxes every future reader.

## Pitfalls
- The Big Rewrite that runs two systems forever because cutover was never designed.
- Refactoring style while behavior-critical mysteries remain uncharacterized.
- Modernizing tech stack without addressing the coupling that made the old one painful.

## Tools & references
"Working Effectively with Legacy Code" (Feathers), strangler-fig pattern (Fowler), scientist-style parallel-run libs.
