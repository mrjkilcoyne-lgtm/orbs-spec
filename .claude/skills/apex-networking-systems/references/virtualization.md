# Virtualization

## Scope
Running guest OSes via hypervisors: KVM, QEMU, virtio, paravirtualization, VM exits, and performance overhead of hardware abstraction.

## Core principles
- VM exits to the hypervisor are expensive (1000s of cycles): every interrupt, device access, page fault, or privileged instruction stalls the guest — the goal of paravirtualization is to batch operations and bypass the hypervisor where possible.
- virtio (para-virtualized drivers) outperform full device emulation by 10x for disk/network: the guest knows it's virtual and cooperates via a shared ring buffer, avoiding context switches per packet.
- EPT (Extended Page Tables) and SLAT (Second Level Address Translation) let the hypervisor manage guest→physical mapping at hardware speed; without them, nested page faults add another VM exit per miss.
- Memory overcommit relies on ballooning (guest releases cold pages to the hypervisor) or transparent page sharing — but you can't exceed physical memory without I/O death spirals; overcommit factors >1.5x are usually wrong.
- Live migration requires dirty-tracking: track which pages the guest modified during a copy phase, so you copy only diffs in later rounds — more rounds = lower downtime but more total bandwidth.

## Apex practices
- Allocate 1 vCPU per physical core in production (2:1 is an overcommit you will regret); hyper-threading is one logical core per physical, not two cores.
- Use `perf` with `kvm:` events to isolate VM exits: sample-based profiling shows where exits cluster (e.g., timer ticks, network I/O), then use KVM tracing to confirm.
- Tune virtio ring sizes and batch-process: smaller rings = lower latency per packet, larger rings = higher throughput; the default is a compromise.
- Pin vCPUs to physical cores and isolate the physical core (via isolcpus, nohz_full) to minimize context switching and TLB flushes.

## Pitfalls
- Overcommitting CPU cores thinking 2:1 works like containerization — it doesn't; vCPUs are scheduled as threads and an oversubscribed core context-switches too often.
- Using shared storage without async I/O readahead: if the guest is thrashing on disk and network I/O multiplexes, add storage-level prefetching or guest read-ahead before blaming the hypervisor.
- Ignoring NUMA on multi-socket hosts: a guest pinned to one socket but accessing memory from another pays NUMA latency; use numactl or libvirt pinning to keep memory and vCPU affine.

## Tools & references
KVM docs, QEMU/libvirt documentation, perf for VM profiling, virtio spec; "Linux Kernel Networking" (Wohlin); Brendan Gregg's performance analysis tools.
