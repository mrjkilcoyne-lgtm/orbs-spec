# Linux Internals

## Scope
The Linux kernel's architecture as it affects engineers: kernel/user split, the major subsystems, /proc and /sys introspection, and how to reason about system behavior from first principles.

## Core principles
- Everything is a file descriptor: files, sockets, pipes, timers (timerfd), events (eventfd), signals (signalfd), processes (pidfd) — the unifying abstraction that lets epoll wait on all of them and makes `lsof`/`/proc/PID/fd` the universal "what is this process touching" tool.
- The kernel is event-driven, not a process: kernel code runs in process context (syscalls), interrupt context (hardware), or deferred work (softirqs, workqueues, kthreads like `ksoftirqd`); high softirq time in `top` means the network/block stack, not "the app", is eating CPU.
- Memory shown by tools is layered fiction: RSS counts shared pages per-process (they sum to more than exist), "free" memory is deliberately near zero because the page cache uses it, and `available` in `free -m` is the number that predicts OOM — teach this or every dashboard lies.
- /proc and /sys are the kernel's live state, not documentation: `/proc/PID/{status,stack,fd,smaps}`, `/proc/pressure/*` (PSI), `/sys/block/*/queue` — reading them beats guessing, and most observability tools are just parsers for them.
- The scheduler, VM, and I/O subsystems interact: a box can be "slow" from CPU contention, memory reclaim (kswapd churning), or I/O wait, and each has distinct signatures — PSI (`/proc/pressure/{cpu,memory,io}`) was added precisely to disambiguate them.

## Apex practices
- Follow the USE method (Gregg): for every resource check Utilization, Saturation, Errors — `vmstat 1`, `mpstat -P ALL 1`, `iostat -xz 1`, `sar -n DEV 1` cover it in four commands before any deep tooling.
- Read kernel behavior at the source of truth: `dmesg -T` for OOM kills, hardware errors, and hung tasks; `/var/log/kern.log`; and know that an OOM kill is logged in dmesg, not by the killed application.
- Use `strace -c` (syscall counts) and `perf top` as first-line profilers: they answer "is it in the kernel or the app, and where" in under a minute; graduate to eBPF tools for production-safe depth.
- Learn one subsystem's tunables deeply per incident: `vm.swappiness`, `vm.dirty_ratio`, scheduler features, `fs.file-max`, `net.core.somaxconn` — but change them from evidence, record the delta, and prefer per-cgroup settings over global knobs.

## Pitfalls
- Chasing "high load average" as CPU: Linux load includes tasks in uninterruptible sleep (D state, usually I/O or NFS hangs), so load 50 on an idle-CPU box means stuck I/O, not compute.
- Tuning by cargo cult: copying sysctl blobs from blog posts (e.g., disabling swap entirely, cranking somaxconn) without knowing the workload; several defaults changed across kernel versions and the blob may now be harmful.
- Ignoring kernel version reality: features like io_uring, cgroups v2, PSI, EEVDF scheduler, and BBR each landed in specific versions — "works on my machine" often means "my kernel is newer"; check `uname -r` first.

## Tools & references
"Linux Kernel Development" (Love), Brendan Gregg's "Systems Performance" (2nd ed.) and linuxperf tools map; man 5 proc, kernel.org documentation tree; vmstat, perf, bpftrace, dmesg.
