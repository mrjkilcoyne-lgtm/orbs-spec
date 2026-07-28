# Synthetic Monitoring

## Scope
Proactive testing from external locations: canary monitoring, uptime checks, and early problem detection.

## Core principles
- Synthetic monitoring detects issues before users report them; a canary that fails alerts the team before customers see errors.
- Uptime checks (ping from multiple locations) verify availability; they're cheap and fast but don't test functionality.
- Canary monitoring (full transaction tests: login, search, checkout) is more realistic but more expensive and fragile (test dependencies).
- Geography matters: uptime checks from multiple regions reveal regional outages that global metrics might hide.
- Synthetic tests have latency overhead (slow, network-dependent); they're good for coarse detection but not for fine-grained performance analysis.

## Apex practices
- Use uptime checks from 3+ geographic locations to verify global availability; this catches regional failures and DNS issues.
- Canary tests should mirror critical user journeys (login, payment, search) but be simple and fast (under 10 seconds).
- Alert on canary failure quickly; a 1-minute detection delay is worthwhile to prevent false alarms.
- Maintain synthetic tests as part of product development; they rot if not updated when flows change.

## Pitfalls
- Canary tests that are too complex (many dependencies, external APIs) and fail for reasons unrelated to your service.
- Canary tests that use test data (test user accounts, test payment methods) and don't detect configuration issues affecting real users.
- Not monitoring canary performance; if canaries are slow, users are slow.

## Tools & references
Pingdom, Datadog Synthetic Monitoring, New Relic Synthetics, Uptime.com, Grafana k6 cloud, canary deployment patterns (Flagger, Argo Rollouts), continuous canary testing.
