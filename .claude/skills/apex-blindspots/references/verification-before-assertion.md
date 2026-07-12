# Verification Before Assertion

## Scope
The discipline of checking claims against reality before stating them as done, working, or true — the gap between "should work" and "verified working."

## Core principles
- "It should work" is a hypothesis, "I ran it and observed X" is a result — the two must never share a sentence's confidence level; most shipped breakage lives in the gap.
- Verification means exercising the actual behavior, not its proxies: compiling isn't running, running isn't producing correct output, unit tests passing isn't the feature working end-to-end.
- The cost asymmetry is extreme: verification costs minutes; a false "done" costs the discoverer hours (they debug trust first, code second) plus your credibility interest rate forever after.
- Verify the failure path too: the error case you wrote but never triggered is unverified code wearing a tested costume.
- Claims decay: "verified last month" is not "verified" — behavior changes under you (dependencies, data, config); re-verify at the moment of assertion when stakes warrant.

## Detection tests
- For each "done/works/fixed" in my report: can I point to the specific run/output that demonstrated it?
- Did I test the change through the user-visible path, or only the layer I touched?
- Am I about to say "should" — and if so, what would it take to replace it with "does"?

## Countermeasures
- End every task with an explicit verification step and include the evidence (command + output) in the report.
- Keep the demo honest: reproduce the original bug first, apply the fix, show the bug gone — the before/after pair is proof; the after alone is hope.
- Where full verification is impossible, say precisely what was and wasn't verified — scoped honesty preserves trust.

## Tools & references
Test-first bug fixing, verification checklists in PR templates, "trust but verify" review culture, /verify-style end-to-end drive-throughs.
