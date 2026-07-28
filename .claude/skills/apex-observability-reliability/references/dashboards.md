# Dashboards

## Scope
Visualizing metrics and logs for decision-making: design for different audiences (operators, management, on-call), alert integration, and avoiding dashboard sprawl.

## Core principles
- A dashboard is a decision-support tool, not a reporting tool; if you're not deciding based on what you see, it's decoration.
- Different audiences need different dashboards: operators want deep drill-down into service details, management wants business-level metrics, on-call wants "is the service healthy?"
- Real-time dashboards (updating every second) are pointless when signals have minutes of latency; refresh rates should match signal speed (metrics every 60s, logs every few seconds).
- Color is not a substitute for clarity; a red graph with no numbers is hard to interpret; combine color with thresholds and actual values.
- Dashboard maintenance is a cost; stale dashboards with unused graphs create technical debt and confusion.

## Apex practices
- Use Grafana for metrics, Kibana/Datadog for logs/traces; each tool is optimized for its domain.
- Design dashboards for specific use cases: "on-call view" (service health, top errors, deploy status), "incident investigation" (detailed timelines, drill-down capabilities).
- Include SLO status on operational dashboards; if an SLI is trending toward breach, operators know to investigate.
- Link dashboards to runbooks and alerts; operators should know "if this graph goes red, do X" without external context.

## Pitfalls
- Dashboard sprawl (100+ dashboards, nobody knows which to look at); consolidate around use cases.
- Vanity metrics (page views, user count) without context (trend, target, SLO); numbers without meaning are noise.
- Dashboards that don't inform action; a graph trending up is useless if you don't know what to do about it.

## Tools & references
Grafana (metrics dashboards), Kibana (log dashboards), Datadog (integrated monitoring), New Relic, dashboard design principles (Heatmap-driven design, Edward Tufte on visualization), dashboard accessibility (color blindness).
