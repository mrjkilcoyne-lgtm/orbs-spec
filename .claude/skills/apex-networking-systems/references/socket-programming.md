# Socket Programming

## Scope
BSD socket API: TCP/UDP connection semantics, buffer management, corner cases, socket options, and portable cross-platform patterns.

## Core principles
- TCP sockets have independent send and receive buffers: SO_SNDBUF and SO_RCVBUF (tunable, kernel-autotuned by default) — a stalled write doesn't block reads, and vice versa; fill both to realize BDP throughput.
- SO_LINGER controls close behavior: setting it to 0 sends RST instead of FIN, which closes immediately but loses in-flight data; the default (linger with timeout) is usually right, and SO_REUSEADDR solves TIME_WAIT address binding.
- Nonblocking sockets return EAGAIN/EWOULDBLOCK instead of blocking, and connect() on non-blocking sockets requires select/poll to detect completion — critical for async frameworks.
- TCP_NODELAY (disable Nagle) reduces latency on request/response: Nagle waits up to 40 ms for a full MSS or ACK of pending data, which stalls small writes; only disable it if you batch writes yourself.
- UDP is connectionless but sockets still have state: connect(2) on a UDP socket filters incoming packets to that peer and is fast (no handshake) — allows MSG_CONFIRM and reduces per-packet overhead.

## Apex practices
- Set SO_REUSEADDR on listeners immediately after socket() to avoid EADDRINUSE after ungraceful shutdown; combined with SO_LINGER (timeout), it allows fast restart.
- Size socket buffers to BDP: buffer_size = throughput (Mbps) × RTT (ms) / 8; verify with `ss -ti` showing SndBuf/RcvBuf and iperf3 showing if you saturate line rate.
- Use TCP_KEEPALIVE to detect dead peers: default 2 hours, but set TCP_KEEPIDLE, TCP_KEEPINTVL, TCP_KEEPCNT for ~5 minute detection (kernel 2.4+).
- Handle SIGPIPE: writing to a closed connection raises SIGPIPE (process dies) unless you set SO_NOSIGPIPE (BSD/macOS) or ignore the signal; use MSG_NOSIGNAL (Linux) in send() calls.

## Pitfalls
- Assuming send() success = delivery: returns only when data lands in the socket buffer, not when the peer receives it; failures surface on the next write or during close.
- UDP datagrams are lossy at the socket level too: if the receive buffer fills, packets drop silently; there's no EWOULDBLOCK for UDP.
- Forgetting that connect() on TCP can block for ~1 minute (SYN retransmit timeout); use nonblocking + select/poll with a timeout for resilient client libraries.

## Tools & references
Stevens' "UNIX Network Programming" Volumes 1–2, man socket(7), man tcp(7), man udp(7); libsocket_wrapper for portable socket abstractions; ping/nc for quick testing.
