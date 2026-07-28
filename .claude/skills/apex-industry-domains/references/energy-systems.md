# Energy Systems

## Scope
Electrical grid, renewable energy integration, smart meters, and demand-side management: real-time balancing, forecasting, and reliability.

## Core principles
- The grid must balance supply and demand instantly: generation = load at every moment (no buffer like batteries used to be rare); imbalance causes outages; voltage and frequency must stay in range.
- Intermittency is the core challenge: wind and solar generation is variable (weather-dependent, time-of-day), so grids must compensate (dispatchable generation, storage, demand response).
- Smart metering (time-of-use pricing, real-time monitoring) enables demand response: customers adjust usage to off-peak hours, reducing peak load and infrastructure cost.
- Forecasting is critical: predicting solar generation (weather forecast → irradiance → power), wind (wind speeds → power), and load (temperature, time, events → consumption) hours ahead allows planning.
- Resilience and redundancy are mandatory: grid failure is catastrophic; N-1 contingency (single component failure doesn't cascade) is standard; blackout investigations reveal design flaws.

## Apex practices
- Build forecasting models (machine learning) for solar, wind, and load; predictions 4–48 hours ahead enable economic dispatch (cheapest generation first).
- Implement demand response automation: smart thermostats and water heaters respond to grid signals (price or frequency) without user intervention; coordination prevents new peak.
- Use real-time phasor data (PMUs: phasor measurement units) for grid monitoring; sampling at 30+ Hz reveals oscillations that SCADA (slower) misses.
- Integrate distributed resources (residential solar, batteries, EVs): they're no longer just loads; they're generation and storage, requiring new communication and control paradigms.

## Pitfalls
- Underestimating renewable variability; a 30% renewable grid is different from 70% (requires massive storage or demand flexibility).
- Ignoring cybersecurity; grid attacks (like Ukraine 2015) can cause widespread outages; operational technology (OT) is separate from IT and requires different security.
- Treating historical load data as representative; climate change and electrification (heat pumps, EVs) change load patterns faster than statistics account for.

## Tools & references
NERC standards (North American grid), IEC 61850 (substation communication), SCADA systems (ABB, Siemens), energy management systems (EMS/SCADA), FERC regulations (US), GreenButton format (smart meter data), NREL (research).
