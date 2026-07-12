# Network Debugging

## Scope
Systematic diagnosis of network issues: packet capture and analysis, kernel tracing, latency isolation, and reproducible test cases.

## Core principles
- Every network issue is in the OS, the cable, or the application — isolate which one first: can you ping? Can you resolve? Can you establish TCP? Can you transfer data? Each answer narrows the space.
- tcpdump (libpcap) captures packets; filters like `tcp and (host 1.2.3.4 or host 5.6.7.8) and port 443` are precise; Wireshark visualizes captures and can follow streams — tcpdump is the first tool, always.
- Kernel tracing (eBPF, kprobes, trace_printk, systemtap) shows what the kernel saw without userspace visibility — TCP retransmits, IP fragments, dropped packets, socket state changes — critical when the NIC counters are silent.
- Latency has components: DNS (name resolution), connect (TCP handshake + packet RTT), TTFB (time to first byte, from request send to first response byte), and throughput (bandwidth-limited window/RTT); isolate each with curl -w or perf.
- Packet loss and reordering are invisible to send/recv — use tcpdump to detect out-of-order sequences or retransmissions; `ss -ti` shows cwnd/ssthresh trends under congestion.

## Apex practices
- Create a reproduction environment: test locally first (same OS/kernel), then in the target environment; network issues are often environment-specific (MTU, PMTUD, firewalls, NAT).
- Tcpdump with `-w <file>` to save and `-r <file>` to replay in Wireshark; filter for your protocol after capture (pcap filters are limited); tshark (CLI Wireshark) for automation.
- Use `ss -ti` to dump live per-connection TCP state: cwnd (congestion window), ssthresh, rtt, retrans — trends tell you if congestion, retransmit storms, or keepalive timeouts are happening.
- Correlate kernel tracing (kprobes on tcp_retransmit_skb) with application logs and timestamps; tail -f /var/log/messages while reproducing, then cross-reference tcpdump timeline.

## Pitfalls
- Assuming a slow network from high latency without checking if it's RTT or loss; a 1 second latency with 1% loss and a 64 KB window caps at ~500 Kbps regardless of link speed.
- Tcpdump drop counter > 0 (see at start of output) means you missed packets; use `-B 1024` (buffer size) or save to disk with `-w` instead of live display to reduce drops.
- Forgetting that client-side DNS caching, browser caches, and NAT timeouts can hide issues; use curl -v --resolve to bypass DNS, and test a fresh connection each time.

## Tools & references
tcpdump, Wireshark/tshark, ss (socket statistics), ip route, traceroute, eBPF tracing tools (tcpdrop, tcpconnect from bcc/libbpf), Linux perf, curl -v -w; Beej's "Guide to Network Programming"; Brendan Gregg's network performance analysis.
