---
name: apex-networking-systems
description: Apex skillset for networking and operating systems internals. Use for TCP/IP, HTTP/1.1-2-3 and QUIC, DNS, BGP routing, firewalls, VPNs and tunneling, Linux internals, processes and threads, memory management, filesystems, syscalls, container internals (namespaces/cgroups), eBPF, virtualization, OS scheduling, I/O models (epoll/io_uring), socket programming, NAT and proxies, IPv6, and network debugging.
---

# Apex Skillset: Networking & Systems

20 areas. Read the matching `references/` file before significant design, implementation, or debugging work in that area.

## Areas
- references/tcp-ip.md — congestion control, handshakes, retransmission
- references/http-protocols.md — HTTP/1.1, HTTP/2, HTTP/3, QUIC
- references/dns.md — resolution, caching, DNSSEC, failure modes
- references/routing-bgp.md — interdomain routing, path selection, hijacks
- references/firewalls.md — netfilter/nftables, stateful filtering, policy design
- references/vpn-tunneling.md — WireGuard, IPsec, overlay networks, MTU
- references/linux-internals.md — kernel architecture, /proc, observability
- references/processes-threads.md — fork/exec, signals, threading models
- references/memory-management.md — virtual memory, page cache, OOM
- references/filesystems.md — VFS, journaling, fsync semantics
- references/syscalls.md — syscall mechanics, vDSO, strace, errno
- references/container-internals.md — namespaces, cgroups v2, OCI runtimes
- references/ebpf.md — verifier, maps, tracing, XDP
- references/virtualization.md — KVM, virtio, paravirtualization, VM exits
- references/os-scheduling.md — CFS/EEVDF, priorities, latency vs throughput
- references/io-models.md — blocking, epoll, io_uring, readiness vs completion
- references/socket-programming.md — socket API, TCP corner cases, buffers
- references/nat-proxies.md — NAT traversal, L4/L7 proxies, connection tracking
- references/ipv6.md — addressing, SLAAC, dual-stack, transition
- references/network-debugging.md — tcpdump, packet analysis, systematic isolation
