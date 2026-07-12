# eBPF

## Scope
Extended Berkeley Packet Filter: in-kernel bytecode execution for networking, tracing, and system observability without kernel modules or restarts.

## Core principles
- eBPF programs run in a kernel VM with a verifier that proves safety: no loops (static instruction limit), no OOB memory access, no kernel pointer leaks — the cost is architectural constraints, not zero-copy magic.
- XDP (eXpress Data Path) hooks at driver rx, before the network stack — microsecond latencies and line-rate packet filtering at the cost of limited packet manipulation and no stack access.
- Maps are the only eBPF→userspace communication: hash, array, ring buffers, percpu variants — sizing matters (max entries bakes into verifier analysis), and BPF_MAP_TYPE_RINGBUF is for events, not high-volume data.
- Kprobes/tracepoints hook deeper into the kernel than XDP but add software overhead; they're ideal for debugging low-frequency events, not for every packet or syscall.
- Tail calls (BPF_PROG_TYPE_TAIL_CALL) chain programs within a 32-call depth limit, used to work around the verifier's instruction limit, not for general control flow.

## Apex practices
- Start with eBPF for observability (tcpconnect, tcpdrop, syscall tracing via bcc/libbpf tools) before writing custom C — the ecosystem is mature and testing is tractable.
- Test the verifier early: run `bpftool prog show` and check for instruction rejection before you scale; the "invalid pointer" error is the verifier protecting the kernel.
- Use libbpf + vmlinux.h for CO-RE (Compile Once Run Everywhere): write once against a vmlinux header and it runs on kernels 5.8+ without relinking, vs bcc which regenerates probes per target kernel.
- Size ring buffers for your event rate; overflow silently discards events — test under load with `bpftool map dump` to catch undersizing.

## Pitfalls
- Writing eBPF for every metric: the verifier's restrictions mean not everything fits; excessive per-packet programs create lock contention and cache misses that undermine the performance gain.
- Assuming XDP is universal: it requires NIC driver support (not all NICs, not Virtio in VMs); test on your target hardware before committing.
- Leaking kernel pointers via BPF_CORE() of internal structures — the verifier blocks direct leaks, but a kprobes program reading kernel memory and writing to a map can expose KASLR.

## Tools & references
libbpf, bcc, bpftool, ebpf.io kernel docs; Brendan Gregg's BPF observability tools (tcpdrop, profile, etc.); "Learning eBPF" (Liz Rice); Cilium eBPF guide.
