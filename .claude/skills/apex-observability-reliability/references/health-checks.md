# Health Checks

## Scope
Liveness, readiness, and startup probes for self-healing: orchestrators use them to restart, drain, or deprioritize unhealthy instances.

## Core principles
- Liveness probes (is the instance alive?) restart dead containers; a broken liveness probe that fires causes a thrashing loop (restart, die, restart).
- Readiness probes (is the instance ready to serve traffic?) temporarily remove unhealthy instances from load balancing without terminating them.
- Startup probes (is the initialization complete?) distinguish slow-starting services from dead services; useful for apps with long startup times.
- Health checks must be fast (< 1 second) and lightweight; if a health check is slow, it'll skew latency and resource usage.
- Health check failures should be actionable; a health check should fail if there's something wrong that operations can fix.

## Apex practices
- Implement liveness checks that verify essential functionality (connectivity to a required dependency), not just "is the process running."
- Implement readiness checks that verify all dependencies are available; a service can be live but not ready if a required database is down.
- Use different endpoints for liveness, readiness, and startup probes; they have different semantics and failure modes.
- Set appropriate timeouts and thresholds (e.g., failure threshold = 3, so a probe must fail 3 times before triggering action).

## Pitfalls
- Health checks that are too strict; failing on temporary network blips causes unnecessary restarts.
- Liveness probes that check dependent services; a dependency outage should not kill the service, only readiness should fail.
- Health check endpoints that are expensive (full database validation); keep checks lightweight.

## Tools & references
Kubernetes probes (liveness, readiness, startup), Docker healthcheck, health check libraries (Spring Boot Actuator, Express health-check), orchestration platforms (Kubernetes, Nomad, Docker Swarm), probe configuration (Kubernetes probe parameters).
