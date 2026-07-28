# Service Mesh

## Scope
Infrastructure layer for service-to-service traffic: sidecars/ambient, mTLS, traffic policy, when it earns its cost.

## Core principles
- A mesh moves cross-cutting network concerns (mTLS, retries, telemetry, routing) from N libraries into platform infrastructure — its value scales with service count and language count.
- The control plane configures, the data plane (Envoy sidecars or ambient node proxies) executes; debugging means knowing which layer misbehaves.
- Zero-trust networking is the killer feature: automatic mutual TLS with workload identity (SPIFFE), authorization policy by service identity not IP.
- Traffic policy as config: canary percentages, retries, timeouts, circuit breaking, fault injection — without touching application code.
- Every request pays the proxy tax (latency, resources, operational complexity); below a few dozen services, libraries and a gateway usually win.

## Apex practices
- Adopt incrementally: mTLS-only first (highest value, lowest risk), then observability, then traffic management.
- Set mesh-level defaults for timeouts/retries and forbid app-level retry duplication (retry multiplication melts systems).
- Use fault injection in the mesh for chaos testing failure paths without code changes.
- Version-pin and canary control-plane upgrades; the mesh is the most privileged component in the cluster.

## Pitfalls
- Adopting a mesh for 8 services because it's on the CNCF landscape.
- Retry policies at mesh + app + client layers compounding into storms.
- Treating sidecar resource overhead as free (it's a per-pod tax you provision).

## Tools & references
Istio (ambient), Linkerd, Cilium mesh, SPIFFE/SPIRE, Envoy docs.
