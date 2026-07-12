# Capacity Planning

## Scope
Forecasting demand, provisioning headroom, and scaling infrastructure to meet growth while maintaining performance and SLOs.

## Core principles
- Capacity is the maximum load a system can sustain at desired performance; beyond capacity, latency spikes and errors occur.
- Headroom (spare capacity) is insurance; a system running at 80% capacity has no buffer for traffic spikes or degradation.
- Forecasting uses historical trends (linear, exponential) and business projections; a new feature or marketing campaign can make forecasts obsolete.
- Scaling models matter: vertical (bigger boxes) has limits and downtime; horizontal (more instances) requires stateless design and load balancing.
- Elasticity (auto-scaling based on demand) can't be instant; spin-up time (1-5 minutes for VMs, 30+ seconds for containers) means you need baseline headroom.

## Apex practices
- Monitor capacity utilization (CPU, memory, disk, network) for every critical resource; CPU at 70-80% is a signal to scale.
- Use growth forecasting tools (trend extrapolation, business metrics) to project when capacity will be exceeded; plan 6+ months ahead.
- Stress test at 2x expected peak load to find bottlenecks (database connections, file handles, memory); fix them before capacity crunch hits.
- Use auto-scaling (Kubernetes HPA, AWS ASG) with lead time: if spin-up takes 3 minutes, configure scaling to kick in at 60% load, not 90%.

## Pitfalls
- Over-provisioning for a spike that never comes (over-confident forecasting).
- Under-provisioning and hitting capacity limits without a plan to scale (no auto-scaling, no runbook for emergency scaling).
- Assuming vertical scaling is an option when reaching database connection limits or ingress NIC saturation (unbounded).

## Tools & references
Capacity planning tools (CloudHealth, Densify, Spot), forecasting (Prophet from Meta), load testing (k6, Gatling, Locust), scaling policies (Kubernetes HPA, AWS EC2 Auto Scaling), trend analysis (Grafana Forecast).
