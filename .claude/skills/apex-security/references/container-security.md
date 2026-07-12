# Container Security

## Scope
Hardening containers across the lifecycle: image construction, registry hygiene, runtime privileges, and Kubernetes-level controls.

## Core principles
- A container is not a security boundary by default — it's namespaces + cgroups sharing the host kernel; a kernel exploit or an over-privileged container (`--privileged`, host PID/network, docker.sock mounted) is host compromise, so defense means shrinking what the kernel exposes (seccomp, capabilities, LSMs).
- Image contents are attack surface: a full distro base ships shells, package managers, and hundreds of CVEs your app never needed — distroless/minimal bases (or scratch for static binaries) remove the attacker's toolkit along with the noise.
- Root in the container is one misconfiguration from root on the host: run as non-root (`USER` directive, `runAsNonRoot: true`), drop all capabilities and add back only what's needed, set `allowPrivilegeEscalation: false` and read-only root filesystem.
- Immutability is the operational security model: containers are rebuilt and redeployed, never patched or exec'd into in prod — which makes drift detectable and "a shell spawned in a container" a high-fidelity alert.
- Trust must be verified at admission: image signature (cosign) and provenance checks in an admission controller ensure only images your pipeline built reach the cluster — a registry compromise otherwise deploys straight to prod.

## Apex practices
- Multi-stage builds: compile in a fat builder image, copy only the artifact into a minimal runtime image; scan the result (Trivy/Grype) in CI with a severity gate and a rebuild cadence so base-image CVEs age out automatically.
- Enforce a baseline via Pod Security Standards (`restricted` profile) or policy engines (Kyverno, OPA Gatekeeper): no privileged pods, no host mounts, required non-root — policy as code, not review-time vigilance.
- Apply default seccomp (`RuntimeDefault`) and an AppArmor/SELinux profile; for hostile or multi-tenant workloads, use kernel-isolation runtimes (gVisor, Kata) or separate node pools.
- Add runtime detection (Falco, eBPF-based tooling) tuned to immutability assumptions: exec into container, unexpected outbound connections, writes to unexpected paths.

## Pitfalls
- Secrets baked into image layers — a deleted-in-later-layer secret is still in the layer history for anyone who can pull the image.
- Mounting `/var/run/docker.sock` into a container (CI runners love this): that socket is unauthenticated root on the host.
- Treating `latest` tags as versioning: unreproducible deploys, un-auditable rollbacks, and admission policies that can't pin anything — use digests.

## Tools & references
Trivy, Grype/Syft, cosign, Kyverno/OPA Gatekeeper, Falco, Kubernetes Pod Security Standards, CIS Docker & Kubernetes Benchmarks, NIST SP 800-190, gVisor/Kata Containers, distroless images.
