# Syscalls

## Scope
The user/kernel boundary: how system calls work, their cost, error conventions, tracing them, and restricting them (seccomp).

## Core principles
- A syscall is a controlled privilege transition: `syscall` instruction → kernel entry, argument validation, dispatch via the syscall table, return with a result or negative errno. Libc wraps this and sets `errno`; the raw kernel convention is a negative return in -1..-4095.
- Syscalls cost more than function calls but less than folklore says: ~100-300 ns baseline, but Spectre/Meltdown mitigations (KPTI) multiplied entry cost on affected CPUs — which is why batching interfaces (readv/writev, sendmmsg, epoll_wait returning many events, io_uring submitting many SQEs per enter) dominate high-performance design.
- The vDSO exists because some "syscalls" aren't: clock_gettime, gettimeofday, getcpu execute in userspace via a kernel-mapped page — so timestamp-heavy code is cheap, and strace not showing your gettime calls is correct behavior, not a bug.
- EINTR is a contract, not an error: slow syscalls can be interrupted by signals and must be retried (or auto-restarted with SA_RESTART); code that treats EINTR as failure produces heisenbugs that appear only under signal load (timers, child exits, profilers).
- Every syscall is attack surface: seccomp-BPF filters restrict the syscall set per-process (Docker's default profile blocks ~44 syscalls, e.g. `keyctl`, `add_key`); pledge/unveil (OpenBSD) and Landlock (Linux) are the same idea — sandboxing is syscall-set minimization.

## Apex practices
- strace fluently: `strace -f -tt -T -e trace=%network` (follow forks, timestamps, per-call duration, category filters), `-c` for the count/latency summary, `-k` for stack traces per call. strace uses ptrace and can slow the target ~100x — for production use `perf trace` or eBPF (syscount, tracepoints) instead.
- Read man pages section 2 for the ERRORS list before handling errors: the difference between EAGAIN/EWOULDBLOCK, EINTR, ENOSPC vs EDQUOT, EMFILE (per-process fd limit) vs ENFILE (system-wide) encodes the correct recovery for each.
- Batch and amortize on hot paths: replace per-item write() with writev, per-packet sendto with sendmmsg, stat storms with statx/openat relative to a dirfd; measure syscall rate with `perf stat -e raw_syscalls:sys_enter`.
- When writing seccomp filters, allowlist from observed behavior (`strace -c` under full test coverage), return ENOSYS or a trap — killing the process on an unexpected syscall — and remember new libc versions change which syscalls get used (open → openat, select → pselect6).

## Pitfalls
- Assuming libc function = syscall: printf buffers (one write per flush, not per call), malloc uses brk/mmap only sometimes, and fork is actually clone — tracing at the wrong layer misattributes behavior.
- Ignoring partial results: read/write may transfer fewer bytes than requested on sockets and pipes (and even files on signals) — every I/O loop needs the "loop until done or error" idiom.
- Short-circuiting fd limits: leaking fds until EMFILE at the default 1024 soft limit, then "fixing" it by raising the limit instead of finding the leak (`ls /proc/PID/fd | wc -l` over time tells the truth).

## Tools & references
man-pages section 2, "The Linux Programming Interface" (Kerrisk), syscall table (arch/x86/entry/syscalls); strace, ltrace, perf trace, bpftrace tracepoints, seccomp(2), libseccomp, Docker seccomp profile.
