# Processes & Threads

## Scope
Process and thread lifecycle on Unix/Linux: fork/exec, wait and zombies, signals, threading models, and inter-process communication.

## Core principles
- On Linux, threads are processes that share: clone() with flags (CLONE_VM, CLONE_FILES, CLONE_SIGHAND) creates both; a "thread" shares address space and fds but has its own tid, stack, and signal mask — which is why `ps -eLf` shows threads and per-thread CPU is visible in /proc/PID/task.
- fork() copies lazily via copy-on-write: cheap even for huge processes, but page-table copying still costs, and forking a multi-GB, multithreaded process is a trap — only the calling thread survives in the child, and any mutex another thread held is locked forever (hence "only async-signal-safe calls between fork and exec").
- Every child must be reaped: wait()/waitpid() collects exit status; unreaped children become zombies (pid-table entries), and orphans are reparented to init/subreaper. PID 1 inside a container inherits the reaping duty — most container zombie plagues come from an app that never expected to be init.
- Signals are asynchronous interrupts with brutal constraints: handlers may only call async-signal-safe functions (no malloc, no printf); modern practice converts signals to fd events via signalfd or a self-pipe so the main event loop handles them synchronously.
- Process groups, sessions, and the controlling terminal govern job control and daemon behavior: Ctrl-C signals the foreground process group, not one process; daemonization (setsid, double-fork) or systemd's supervision exists to detach from these semantics deliberately.

## Apex practices
- Prefer posix_spawn or fork+exec immediately over bare fork for launching programs; in threaded programs treat fork-without-exec as forbidden.
- Use pidfds (pidfd_open, CLONE_PIDFD) to manage child processes race-free — PIDs recycle, and kill(pid) after a recycle kills an innocent process; pidfds close that TOCTOU hole.
- Design shutdown as a signal protocol: SIGTERM → stop accepting work, drain, exit; SIGKILL as the supervisor's deadline enforcement. Test that your service exits within the orchestrator's grace period (Kubernetes default 30 s) or data loss is scheduled.
- Choose the concurrency unit by isolation need: processes for fault/security isolation (browser tabs, prefork servers), threads for shared-memory parallelism, and know the memory cost — default thread stack is 8 MB virtual on Linux (`ulimit -s`), so thousands of threads are fine virtually but scheduler-expensive.

## Pitfalls
- Zombie leaks from ignoring SIGCHLD or forgetting waitpid in a loop (multiple children can collapse into one SIGCHLD delivery — always `while (waitpid(-1, ..., WNOHANG) > 0)`).
- Calling non-async-signal-safe code in handlers — the deadlock where a SIGTERM handler calls the logger, which takes the malloc lock the interrupted thread already holds, fires rarely and only in production.
- Sharing state across fork unintentionally: duplicated file offsets (parent and child share the open file description), both processes flushing the same stdio buffer (double output), or a forked RNG/connection pool producing identical "random" values and interleaved protocol garbage.

## Tools & references
"Advanced Programming in the UNIX Environment" (Stevens & Rago), "The Linux Programming Interface" (Kerrisk); man 2 clone/fork/wait/signal-safety(7); strace -f, ps -eLf, /proc/PID/task, pidfd_open(2).
