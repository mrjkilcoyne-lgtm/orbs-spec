# TCP/IP

## Scope
The TCP/IP stack: IP addressing and fragmentation, TCP connection lifecycle, reliability, flow control, and congestion control.

## Core principles
- TCP provides a reliable byte stream, not messages: one send() can arrive as several reads and vice versa — any protocol on TCP needs its own framing (length prefix or delimiter).
- Congestion control is the heart of TCP: slow start, congestion avoidance, fast retransmit/recovery. Modern kernels default to CUBIC; BBR models bandwidth×RTT instead of treating loss as the congestion signal, which matters on lossy or long-fat paths.
- Throughput is bounded by window/RTT: a 64 KB window over 100 ms RTT caps at ~5 Mbps regardless of link speed — window scaling (RFC 7323) and right-sized buffers are how you fill long fat networks (bandwidth-delay product).
- Connection teardown is asymmetric: the side that closes first holds TIME_WAIT for 2×MSL (60 s on Linux), which exhausts ephemeral ports on clients making rapid short connections — a reason servers should usually close first, and clients should pool.
- Path MTU discovery relies on ICMP "fragmentation needed" arriving; firewalls that drop all ICMP create black holes where small packets pass and full-size ones vanish — the classic "SSH works, SCP hangs" signature.

## Apex practices
- Set TCP_NODELAY for request/response protocols: Nagle's algorithm interacting with delayed ACK adds up to 40 ms stalls on small writes; batch writes yourself instead of relying on the kernel.
- Use `ss -ti` to read live per-connection state — cwnd, ssthresh, rtt, retrans — before theorizing; retransmits and shrinking cwnd distinguish congestion from application slowness.
- Enable SO_REUSEADDR on listeners always; treat `tcp_tw_reuse` and shortened FIN timeouts as targeted client-side fixes, not global defaults.
- Size kernel buffers via `net.ipv4.tcp_rmem/tcp_wmem` autotuning maxes for high-BDP paths; verify with iperf3 that you actually reach line rate before blaming the app.

## Pitfalls
- Assuming send() success means delivery — it only means the data reached the local socket buffer; the peer may never see it, and the failure surfaces on a later write as ECONNRESET or EPIPE.
- Ignoring SYN backlog: when `somaxconn`/listen backlog overflows, Linux silently drops SYNs and clients see mysterious multi-second connect delays (SYN retransmission timer), not errors.
- Debugging "slow network" without separating RTT, loss, and throughput — each has different causes and fixes; loss on the path looks identical to bufferbloat in latency graphs until you look at retransmissions.

## Tools & references
Stevens' "TCP/IP Illustrated Vol. 1", RFC 9293 (TCP), RFC 7323, BBR paper (Cardwell et al., ACM Queue 2016); tcpdump, ss, iperf3, tc/netem.
