# Silent Failures

## Scope
Failures that produce no signal: swallowed exceptions, ignored return codes, undrained DLQs, partial successes reported as success — the system lying about its own health.

## Core principles
- Silence is a design decision made by omission: every catch-and-continue, unchecked error return, and fire-and-forget task is someone choosing (usually unconsciously) that this failure isn't worth knowing about — the blindspot is that nobody remembers deciding.
- Partial success is the deadliest shape: 990 of 1000 rows imported, 3 of 4 notifications sent, cache updated but index not — the operation "succeeded," the user sees success, and the corruption compounds until it surfaces somewhere unrelated weeks later.
- Failure signals decay along the path: the exception becomes a log line becomes a warning-level entry in a log nobody tails becomes nothing — each hop needs an explicit decision: page, alert, log-with-review, or (deliberately, documented) ignore.
- Background work fails invisibly by default: cron jobs, queue consumers, async tasks have no user watching; without dead-man switches ("alert if the job DIDN'T run") a dead scheduler is indistinguishable from a quiet day.
- The absence of errors is not the presence of health: zero error logs can mean zero errors or a dead logging pipeline; monitoring must include heartbeats and expected-activity checks (business-metric floors: "orders per hour never zero on a weekday").

## Detection tests
- Grep for the swallow patterns: empty catch blocks, `except: pass`, ignored err returns, `.catch(() => {})` — each is a decision to audit.
- For each batch/multi-step operation: what does the caller see when step 3 of 4 fails?
- If this cron/consumer died right now, what would notice, and when?

## Countermeasures
- Make the null-handler impossible: lint rules against empty catches, must-use result types (Rust's #[must_use], Go errcheck), and code review treating error paths as first-class.
- Dead-man switches on all scheduled/background work (healthchecks.io pattern) and DLQ depth alerts with an owner.
- Report partial results honestly in APIs and UIs: succeeded/failed counts with retryable failure detail — never collapse to a boolean.

## Tools & references
errcheck/must-use lints, healthchecks.io / dead-man's-snitch pattern, DLQ alerting, "crash-only" design papers, absence-alerting in Prometheus (absent()).
