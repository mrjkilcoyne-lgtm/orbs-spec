# OS Scheduling

## Scope
Kernel scheduling policy: CFS and EEVDF, time slices, priorities, load balancing across cores, and latency vs throughput tradeoffs.

## Core principles
- CFS (Completely Fair Scheduler, Linux 2.6.23+) and EEVDF (Earliest Eligible Virtual Deadline First, Linux 6.6+) aim to make all tasks progress fairly relative to their weight — not equally, but proportional to nice/weight; a niced task gets fewer cycles but same %time.
- Preemption latency (wake-up to running) is driven by time slice: default slice ~6–48 ms depending on load and priority; reducing it cuts latency but increases context-switch overhead (cache thrashing, TLB flushes).
- load_balance() runs every 1–10 ms and moves tasks between cores to minimize idle time; on systems with many cores, this can create thundering-herd wakeups (everyone running one task).
- Real-time tasks (SCHED_FIFO, SCHED_RR) have no fairness guarantees — they preempt everything else and can starve normal tasks; use sparingly.
- Affinity (taskset, cpuset) reduces migration overhead but can create hotspots; the scheduler's automatic load balancing is often smarter than hardcoding pins.

## Apex practices
- Measure preemption latency with `cyclictest`: jitter <100 µs is good, >1 ms means context-switch storms or priority inversion — check for high-frequency system tasks or RT tasks.
- Use systemd's CPUQuota (or cgroups) for coarse resource limits instead of nice values, which are proportional-share (a niced task doesn't get fewer cycles, just fewer than default).
- For low-latency workloads, enable isolcpus + nohz_full: carve out cores for your app and disable the timer tick to avoid periodic wakeups (Linux 4.0+).
- Profile with `perf sched`: record context switches and latencies, then `perf sched timehist` to see what preempted what and for how long.

## Pitfalls
- Assuming lower nice value = faster execution (it doesn't; it means a proportional-share increase relative to other tasks).
- Pinning all threads to the same core(s) to "improve cache" without understanding the hidden load-balance suppression; let the scheduler spread work unless you have measured contention.
- Priority inversion: high-priority task blocks waiting for a low-priority task holding a lock; mutexes with priority inheritance (PI locks) mitigate this but aren't free.

## Tools & references
CFS/EEVDF scheduler code and docs, `sched-domains` analysis, perf sched, cyclictest, tuna, systemd resource-control docs; "Timekeeping and Scheduling" in Linux Kernel Development (Love).
