# Container Internals

## Scope
What containers actually are on Linux: namespaces, cgroups, union filesystems, and the runtime stack (OCI, runc, containerd) — the mechanics beneath Docker and Kubernetes.

## Core principles
- A container is a process with different views and limits, not a VM: namespaces change what it sees (pid, net, mnt, uts, ipc, user, cgroup, time — 8 kinds), cgroups limit what it uses, and capabilities+seccomp+LSM restrict what it may do. There is no "container" object in the kernel.
- cgroups v2 unified the hierarchy and fixed v1's split-brain: one tree, `memory.max`/`memory.high`, `cpu.max` (quota/period), `io.max`, and PSI pressure metrics per group. CPU limits are throttling, not reservation: a 0.5-CPU quota with 100 ms period means 50 ms runtime then a forced 50 ms stall — the source of tail-latency cliffs in "CPU-limited" services.
- The user namespace is the security lynchpin: root in the container maps to an unprivileged uid on the host (rootless containers); without it, container root is host root gated only by capabilities and seccomp — most container escapes exploit that gap plus a mounted host surface (docker.sock, /proc, host paths).
- Images are layered copy-on-write mounts: overlayfs stacks read-only layers under a writable upper dir; a file "deleted" in an upper layer is a whiteout, writes to lower-layer files trigger copy-up (first-write latency on big files), and layer ordering is why Dockerfile instruction order controls cache hits.
- Inside a container, PID 1 is your process with init's obligations and none of its defaults: it must reap orphans and handle SIGTERM explicitly (kernel default handlers for PID 1 ignore signals) — the reason `tini`/`docker run --init` and "my container takes 10 s to stop" (SIGKILL after grace) exist.

## Apex practices
- Reproduce container primitives by hand once: `unshare -Urnmpf --mount-proc`, `ip netns`, and writing to `/sys/fs/cgroup` teach more than any diagram; `nsenter -t PID -a` is the production tool for entering a running container's namespaces without docker exec.
- Set memory limits with headroom for the page cache and know that cgroup OOM kills the container's processes silently from the app's view — check `memory.events` (oom_kill counter) and dmesg; set requests=limits or use `memory.high` for pre-OOM throttling.
- Watch CPU throttling explicitly: `cpu.stat`'s nr_throttled/throttled_usec (or container_cpu_cfs_throttled_* metrics); if a latency-sensitive service is throttled, raise the quota or remove limits and rely on cpu.weight (shares) — throttling with idle host CPU is a config bug, not a capacity problem.
- Minimize the sandbox surface deliberately: drop capabilities to the needed set (most apps need none beyond NET_BIND_SERVICE), keep the default seccomp profile on, mount root filesystems read-only, and never mount docker.sock into a container you don't fully trust.

## Pitfalls
- Resource-blind runtimes: JVMs/Go/Python reading host CPU count and memory instead of cgroup limits — modern JVMs (UseContainerSupport) and Go 1.25+ (GOMAXPROCS cgroup-awareness) handle it, but older runtimes spawn 64 GC threads in a 0.5-CPU container.
- Trusting /proc inside containers: /proc/meminfo and /proc/cpuinfo show host values (lxcfs exists to fake them), so in-container monitoring agents report host memory and autoscaling logic reads garbage.
- Conflating image and runtime security: scanning images while running containers as privileged, with host network, or with writable host mounts — the runtime flags, not the CVE list, are where escapes happen.

## Tools & references
man 7 namespaces/cgroups/capabilities, cgroups v2 kernel docs, OCI runtime/image specs; unshare, nsenter, crictl, ctr, systemd-cgtop, dive (image layers); "Container Security" (Liz Rice).
