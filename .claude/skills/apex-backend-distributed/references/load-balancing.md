# Load Balancing

## Scope
Distributing traffic across instances: L4 vs L7, algorithms, health checks, session concerns.

## Core principles
- L4 (connection-level) is fast and dumb; L7 (request-level) understands HTTP — routing, retries, and per-request balance need L7 (critical for HTTP/2/gRPC multiplexed connections).
- Algorithm matters under heterogeneous load: round-robin assumes uniform requests; least-outstanding-requests adapts; power-of-two-choices scales without global state.
- Health checks define availability: shallow (port open) catches crashes, deep (dependency-aware) catches zombies — but deep checks that fan out can cascade a partial outage into a full one.
- Sticky sessions are a design smell: externalize session state so any instance serves any request; affinity only for genuine in-memory state (websockets, shards).
- The balancer is a single point of failure unless it isn't: HA pairs, anycast, or DNS-level distribution above it.

## Apex practices
- Drain before removing: connection draining on deploys/scale-in so in-flight requests finish.
- Slow-start new instances (warmup weight ramp) — cold caches and JIT make fresh instances slower, and naive balancing overloads them.
- Balance retries with budgets and only on safe/idempotent requests; retry storms amplify outages through the balancer.
- Zone-aware balancing to keep traffic local and survive AZ failure with capacity math done in advance.

## Pitfalls
- gRPC/HTTP2 through an L4 balancer: one connection, one backend, zero balance.
- Health check thresholds that flap instances in and out under load.
- Marking all backends unhealthy → some balancers fail open, some closed — know yours.

## Tools & references
Envoy/nginx/HAProxy docs, cloud LB docs (ALB/NLB), Google SRE book load-balancing chapters, power-of-two-choices paper.
