# Queueing Theory

## Scope
Modeling systems with arrival/service processes: M/M/1 queues, Little's law, stability, and performance metrics for resource allocation.

## Core principles
- Little's law (L = λW) is empirical and powerful: average number in system = arrival rate × average time in system; it holds for nearly any queue and requires no distributional assumptions.
- An M/M/1 queue (Poisson arrivals, exponential service, 1 server) is fully solvable; stability requires λ < μ (arrival rate < service rate); under stability, average queue length is λ/(μ−λ).
- Utilization ρ = λ/μ; as ρ → 1, queues grow unbounded; doubling capacity (μ) has much more impact than slightly reducing arrivals.
- Service time distributions matter: exponential (memoryless, high variance) is different from deterministic (low variance); same λ and μ but different service distributions produce different queue lengths.
- Renewal theory underpins queueing: if you can't assume Markovian (exponential) arrivals/service, renewal processes still enable tail bounds and approximations.

## Apex practices
- Use M/M/1 as a baseline model; deviations (M/M/c for multiple servers, M/G/1 for general service) require more complex analysis but often have closed forms.
- Simulate to understand non-Markovian systems or high-dimensional queuing networks; simulation is faster than exact analysis for complex interactions.
- Design systems to keep utilization ρ < 0.8 if predictable response time matters; exponentially-distributed delays hide behind average metrics.
- Apply queueing models to CPU scheduling, network routing, and resource provisioning: recognizing a system as a queue clarifies bottlenecks.

## Pitfalls
- Confusing M/M/1 assumptions (Poisson arrivals, exponential service) with real-world data (often bursty with heavy tails); approximations fail badly on edge cases.
- Ignoring non-linear effects in multi-server queues; adding a second server to an M/M/1 doesn't just halve wait times.
- Assuming arrival rates are constant; real systems have cycles (time-of-day, seasonal); overprovisioning for peak is necessary.

## Tools & references
Gross-Harris "Fundamentals of Queueing Theory," Kleinrock's seminal papers, Kendall notation (A/B/c/N/K/D), discrete-event simulation frameworks.
