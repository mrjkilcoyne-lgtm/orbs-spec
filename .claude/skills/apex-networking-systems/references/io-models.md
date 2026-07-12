# I/O Models

## Scope
Kernel-level I/O notification: blocking, select/poll, epoll, io_uring, readiness vs completion models, and when each model fits.

## Core principles
- Blocking I/O (read/write) suspends the process until data is ready — simple but unscalable (one thread per connection); useful for serial work but wasteful for high concurrency.
- Readiness models (select, poll, epoll) notify when an fd is ready for I/O but don't transfer data — the application still calls read/write — and epoll scales to 10k+ connections via red-black trees and callback chains; poll(2) scans all fds per call, O(n), vs epoll's O(1) per event.
- io_uring (Linux 5.1+) is a completion model: queue an operation (read, write, accept, etc.) and the kernel completes it asynchronously into a shared ring buffer — no syscall per operation, batching reduces overhead; the cost is API complexity and ordering semantics you must respect.
- The kernel's buffer managment varies: epoll/poll copy buffers into kernel space, then userspace reads them again; io_uring with IORING_OP_READ_FIXED pins memory and reads directly, avoiding one copy in high-throughput paths.
- Event-loop architecture matters: epoll can starve writers if you block on a slow reader; a good reactor alternates between processing and waiting, or uses separate read/write loops.

## Apex practices
- Start with epoll for most async I/O; it's O(1) per event, well-optimized in production kernels, and the POSIX semantics are stable across platforms (Linux, BSD).
- Use level-triggered epoll (default) for simplicity — re-queues fds that remain ready; edge-triggered requires careful handling to avoid missing events in slow consumers.
- io_uring shines for storage I/O (NVMe, database) and high-frequency RPC where syscall overhead matters — measure latency with and without fixed buffers before committing.
- Debug readiness models with `strace -e epoll_wait` to see event volume and latency; high-frequency re-arming (same fd repeatedly ready) suggests a backlog or buffer size issue.

## Pitfalls
- Blocking reads/writes on a single thread with multiple connections (use a thread per connection or async I/O instead).
- Edge-triggered epoll without fully draining an fd (read until EAGAIN), causing events to vanish even though data is waiting.
- io_uring memory pinning exhausting memory limits; pin only the buffers you know will be hot.

## Tools & references
man epoll(7), man io_uring(7), liburing, libuv, ASIO documentation; "The Linux Programming Interface" (Kerrisk) chapters on I/O multiplexing; io_uring blog posts (Ming Lei).
