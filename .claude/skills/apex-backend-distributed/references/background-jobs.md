# Background Jobs & Scheduling

## Scope
Work outside the request cycle: job queues, retries, cron, exactly-once-ish execution.

## Core principles
- Anything slower than ~1s or failure-prone doesn't belong in the request path: enqueue, return, process async — the queue is the shock absorber.
- Jobs run at-least-once: workers crash mid-job and the job re-runs; every job body must be idempotent or guarded (unique keys, conditional transitions).
- Retries need design, not defaults: exponential backoff + jitter, max attempts, then DLQ with alerting — and distinguish retryable (timeout) from permanent (validation) failures immediately.
- Queues need priorities/lanes: one slow bulk-import type can starve password-reset emails behind it; separate queues per latency class.
- Scheduled (cron) work needs a distributed answer: leader election or lock (or the platform's scheduler) so N instances don't run it N times, plus catch-up policy for missed windows.

## Apex practices
- Enqueue transactionally with the state change (outbox or same-DB job table) — "saved but never enqueued" is the classic silent failure.
- Set job timeouts + heartbeats so stuck jobs get reaped and retried instead of zombie-blocking a worker forever.
- Instrument the four golden job metrics: queue depth, processing latency, failure rate, retry age of oldest job.
- Make jobs small and resumable: chunk the million-row backfill with checkpoints; one 6-hour job is one 5h59m failure waiting.

## Pitfalls
- Passing full objects in the payload instead of IDs (stale data processed after state changed — re-fetch inside the job).
- Cron jobs with no overlap protection running concurrently after a slow run.
- Silent DLQs: failed jobs accumulating for weeks with no alert.

## Tools & references
Sidekiq/Celery/BullMQ docs, Temporal for workflow-grade jobs, cloud schedulers, transactional outbox pattern.
