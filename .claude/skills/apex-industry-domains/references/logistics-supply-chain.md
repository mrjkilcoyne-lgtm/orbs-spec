# Logistics & Supply Chain

## Scope
Movement of goods across network: planning (routing, scheduling), tracking, warehouse operations, and optimization of cost and speed.

## Core principles
- Routing is combinatorial NP-hard (traveling salesman problem): optimal routes require constraints (time windows, vehicle capacity, driver shifts); approximation algorithms are necessary.
- Last-mile delivery (final step to customer) is the most expensive (40–50% of total cost); route density matters (urban ≪ rural cost per stop); algorithms must minimize empty miles.
- Inventory is a tradeoff: too much ties up capital and storage cost; too little causes stockouts and customer loss; demand forecasting is critical.
- Visibility (tracking) is customer expectation: real-time tracking from pick to delivery; systems integrate GPS, scanners, and delivery-driver apps.
- Multi-echelon networks are common: factories → distribution centers → warehouses → stores → customer; optimization across all layers is complex.

## Apex practices
- Use vehicle routing software (VRP: Google OR-Tools, Optaplanner) rather than greedy heuristics; algorithm maturity matters enormously (10% better routing = millions saved).
- Implement granular tracking (scanned at every checkpoint): warehouse in/out, vehicle load/unload, delivery attempt; granularity enables diagnosis and customer confidence.
- Forecast demand using historical sales and external signals (weather, events, promotions); demand forecasting directly affects inventory levels and route planning.
- Design warehouses for throughput (flow: receive → sort → ship) not storage; a warehouse designed around storage is slow and inflexible.

## Pitfalls
- Underestimating last-mile complexity; coverage and timing are hard constraints, not suggestions.
- Ignoring demand seasonality; Black Friday, holidays, and regional events cause spikes that break assumptions.
- Failing to track exceptions (failed deliveries, misroutes, damaged goods); they're the real cost drivers, not average case.

## Tools & references
SAP Supply Chain, Oracle, Flexport (freight), API integration (FedEx, UPS, DHL), vehicle routing (Google OR-Tools, Optaplanner), warehousing systems (WMS: Manhattan, 3PL software).
