# Confirmation Bias

## Scope
Seeking, noticing, and over-weighting evidence that supports the current hypothesis — in debugging, research, design validation, and metrics reading.

## Core principles
- The bias operates at search time, not just judgment time: which logs you grep, which users you interview, which query you run first — the evidence stream is pre-filtered before "objective" evaluation begins.
- Hypotheses earn keep by surviving falsification attempts, not by accumulating consistent anecdotes: consistent evidence is cheap (most evidence is consistent with most hypotheses); discriminating evidence is what pays.
- In debugging it looks like: finding one plausible cause and stopping the search — the first satisfying explanation ends investigation while the actual bug watches from the next file.
- In product it looks like: demo-driven validation — showing users the happy path and hearing yes, versus watching them attempt the task cold.
- Wason's lesson: people test rules by picking confirming cases (2-4-6 problem); the trained move is proposing the case your hypothesis says should FAIL and checking it does.

## Detection tests
- What result would prove me wrong, and have I actually run that specific check?
- Did I stop investigating at the first coherent story?
- Am I explaining away disconfirming data ("probably noise," "edge case") faster than confirming data?

## Countermeasures
- Write the hypothesis down, then design the test that kills it (not the test that flatters it) — one falsification attempt per hypothesis, minimum.
- Generate a rival hypothesis before evaluating the first; competition disciplines evidence-weighing.
- In reviews and analytics, look for the strongest disconfirming case deliberately: the churned user, the failing input, the quarter that bucks the trend.

## Tools & references
Wason selection task literature, differential diagnosis method, "strong inference" (Platt), pre-registered analysis plans.
