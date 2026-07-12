# Debugging

## Scope
Systematically isolating the cause of a defect from its symptom.

## Core principles
- Reproduce first: an unreproduced bug can't be verified fixed.
- Form a hypothesis, design the cheapest experiment that could falsify it, repeat — no shotgun changes.
- Bisect the space: half-split over commits (git bisect), code path, data, and environment.
- Read the error message. Then read it again. Most clues are ignored, not hidden.
- The bug is usually in your code, then your understanding, then dependencies, and almost never the compiler.

## Apex practices
- Build a minimal reproduction; the act of minimizing usually reveals the cause.
- Instrument with structured evidence (logs, counters) rather than staring; make the invisible visible.
- Keep a written log of hypotheses tried during long hunts — it prevents loops and helps the postmortem.
- After the fix, ask: why did this survive tests and review? Patch that hole too.

## Pitfalls
- Fixing the symptom where it appears instead of the cause where it originates.
- Changing multiple variables per experiment, learning nothing.
- "It works now" without understanding why it failed — the bug will return.

## Tools & references
Debuggers (gdb/lldb, IDE), git bisect, rr/time-travel debugging, "Debugging" by David Agans (9 rules).
