# Automotive Embedded

## Scope
Vehicle software and systems: safety-critical real-time control, hardware integration, compliance (FMEA, ISO 26262), and over-the-air updates.

## Core principles
- Safety is existential: a bug in braking or steering can kill people; all safety-critical systems must use ASIL (Automotive Safety Integrity Level: A–D) and follow ISO 26262 (functional safety standard).
- Real-time constraints are hard: ECU (electronic control unit) firmware must respond in microseconds (fuel injection, ABS); missing a deadline is a failure, not a slow response.
- Hardware is fixed post-manufacture: a vehicle released to customers cannot be redesigned; bugs found in the field are expensive (recalls), so design and testing are conservative and thorough.
- OTA (over-the-air) updates are now common: vehicles connect (cellular, WiFi) and download firmware patches; updates must be fail-safe (can't brick vehicles if power lost mid-update).
- Interoperability is complex: dozens of ECUs (engine, transmission, infotainment, safety) on different buses (CAN, FlexRay, Ethernet) must coordinate.

## Apex practices
- Use formal verification for safety-critical logic: model checking and theorem proving provide stronger guarantees than testing.
- Implement watchdog timers: if a process hangs, watchdog reboots the ECU; graceful degradation replaces full failure.
- Design OTA updates with rollback: verify downloaded firmware before applying, keep previous version in storage, and revert if new version fails to boot.
- Use FMEA (Failure Mode and Effects Analysis) to identify failure modes and their consequences; ISO 26262 requires systematic risk assessment.

## Pitfalls
- Assuming automotive-grade hardware is infallible; components have temperature, vibration, and electromagnetic tolerances; margins are tight.
- Mixing safety-critical and non-safety code in the same process; a crash in infotainment should not crash the engine control unit.
- Underestimating integration complexity; testing a single ECU is feasible; testing all ECUs and their interactions across variants is not.

## Tools & references
ISO 26262 (functional safety standard), ASIL definitions, AUTOSAR (automotive middleware standard), CAN protocol, diagnostic standards (UDS, OBD), testing frameworks (ADAS simulation, HIL: hardware-in-the-loop).
