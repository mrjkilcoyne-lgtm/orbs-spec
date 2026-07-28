# Memory Management

## Scope
Virtual memory on Linux: paging, the page cache, overcommit and OOM, huge pages, swap, and how allocators interact with the kernel.

## Core principles
- Virtual memory is a mapping, not a reservation: mmap/malloc return address space; physical pages materialize on first touch via page faults. This is why RSS < VSZ, why overcommit works, and why "allocated successfully" can still die on touch under memory pressure.
- The page cache is the main consumer of "free" RAM by design: all file I/O flows through it (unless O_DIRECT), dirty pages are written back by flusher threads governed by `vm.dirty_ratio`/`dirty_background_ratio`, and dropping it (echo 3 > drop_caches) is a diagnostic, not an optimization.
- Linux overcommits by default (`vm.overcommit_memory=0` heuristic), and the OOM killer is the enforcement mechanism: it scores processes (oom_score, badness ≈ memory used, adjusted by oom_score_adj) and SIGKILLs the winner — your database dying at 3am with "Killed" in dmesg is this, not a crash.
- Reclaim has an ordering and a cost: clean page cache is dropped free; dirty pages must be written back; anonymous pages need swap. With no swap, anonymous memory is unreclaimable and pressure converts directly into cache thrashing then OOM — a small swap space plus `vm.swappiness` tuning often outperforms swap-off dogma (and zswap/zram change the math again).
- TLB reach matters at scale: 4 KB pages mean huge working sets thrash the TLB; explicit hugepages (2 MB/1 GB) help databases, while Transparent Huge Pages help some workloads and famously hurt others (latency spikes from khugepaged compaction — many databases recommend `madvise` or off).

## Apex practices
- Diagnose with the right counters: `free -m` "available" (not "free"), `smem`/`/proc/PID/smaps_rollup` for PSS (proportional shared) when processes share pages, PSI (`/proc/pressure/memory`) for stall time, and `sar -B`/`vmstat` for fault and reclaim rates.
- Set memory limits via cgroups v2 (`memory.max`, `memory.high`) rather than ulimits: `memory.high` throttles-and-reclaims before the hard kill, and per-cgroup pressure isolates a leaky service from the box.
- Control OOM outcomes deliberately: protect critical daemons with `oom_score_adj=-1000` sparingly, prefer sacrificial ordering (kill the cache before the database), and use systemd-oomd/earlyoom with PSI thresholds for userspace pre-emption before kernel OOM's freeze-then-kill.
- Know your allocator: glibc malloc arenas inflate RSS in threaded apps (MALLOC_ARENA_MAX), jemalloc/tcmalloc return memory differently (madvise MADV_FREE keeps RSS looking high until pressure), so "RSS grew" needs allocator-level evidence (`malloc_stats`, jemalloc `stats.print`) before "memory leak" is declared.

## Pitfalls
- Reading RSS as "the app's memory": shared libraries and page cache mappings are counted in every process; summing RSS across processes overstates wildly — use PSS for attribution.
- Running latency-sensitive databases with THP=always and default NUMA policy on multi-socket boxes: khugepaged stalls and cross-node access produce mysterious multi-ms latency spikes; check `numactl --hardware` and THP settings first on such hosts.
- mlock/overcommit blind spots: assuming malloc failure is the memory-out signal (with overcommit it usually isn't — the kill comes later on touch), or disabling overcommit (`=2`) on a system sized for it and breaking every fork of a large process.

## Tools & references
"Systems Performance" ch. 7 (Gregg), kernel docs Documentation/admin-guide/mm/; free, smem, vmstat, pmap, /proc/meminfo and smaps, bpftrace memory tools; jemalloc/tcmalloc tuning guides.
