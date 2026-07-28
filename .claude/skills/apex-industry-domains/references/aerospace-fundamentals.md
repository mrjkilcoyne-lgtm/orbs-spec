# Aerospace Fundamentals

## Scope
Aircraft systems, satellite operations, and guidance systems: reliability, redundancy, and safety in extreme environments.

## Core principles
- No single-point failure is allowed: critical systems (controls, power, hydraulics) must have independent backups; triple redundancy is common (vote on outputs, use majority).
- Environmental extremes are design drivers: -55°C to +125°C operating temperature, radiation in space, electromagnetic interference at altitude; components must be qualified for these ranges.
- Testing is exhaustive and expensive: a software patch for an airliner takes months of testing and certification; field updates (OTA) are rare due to lack of easy connectivity and ground infrastructure.
- Human factors are critical: pilots are users; systems must support manual override and provide clear feedback; automation surprises (mode confusion, hidden modes) cause accidents.
- Certification is a process: FAA/EASA certify aircraft before they fly passengers; avionic software must meet DO-178C (airborne software standards); regulatory approval is part of the development schedule.

## Apex practices
- Implement voting logic: three independent channels measure altitude, for example; software votes on the result and alerts pilots if discrepancy is detected.
- Use formal methods (model checking) for critical control logic; testing alone cannot guarantee correctness.
- Design manual modes: pilots must be able to fly the aircraft without computers; modern aircraft have autopilot and fly-by-wire, but manual reversion is still possible.
- Trace all requirements to code to tests to certification: DO-178C enforces traceability; every requirement must be implemented and tested.

## Pitfalls
- Assuming modern computers are reliable; radiation in space causes bit flips; mitigation (error-correcting memory, watchdogs) is standard but not free.
- Overcomplicating automation; the A320 has automation surprises (modes not obvious to pilots) that have contributed to accidents; simplicity and predictability are features.
- Ignoring electromagnetic compatibility; a single device emitting interference can disrupt critical systems.

## Tools & references
DO-178C (airborne software certification), DO-254 (avionic hardware certification), MIL-HDBK-1908 (environmental testing), FAA/EASA certification processes, formal methods (SCADE, Nusmv), redundancy architectures.
