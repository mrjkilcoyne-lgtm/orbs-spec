# Agritech

## Scope
Agricultural technology: crop monitoring, farm operations, weather integration, soil and irrigation optimization, and connecting farmers to markets.

## Core principles
- Farming is seasonal and weather-dependent: decisions (planting date, irrigation timing, harvest window) depend on forecast and historical data; a week's delay can halve yield.
- Heterogeneity is real: soil, microclimate, and pest pressure vary by field (even within a single field); one-size-fits-all recommendations fail; precision agriculture is tailored to location.
- Data sources are messy: weather stations are sparse (interpolation required), soil sensors degrade, equipment (tractors, sprayers) have no standard telemetry, farmer behavior is non-trivial.
- Connectivity is limited: rural areas lack broadband; systems must work offline and sync when connectivity returns; cloud-only systems fail in the field.
- Adoption friction is high: farmers are skeptical, data literacy varies, and they optimize for (multiple goals: yield, cost, sustainability, resilience); recommendation engines must respect farmer constraints.

## Apex practices
- Integrate weather forecasting (NOAA, proprietary high-resolution models) and historical weather data (satellite, station networks) for microclimate modeling.
- Implement offline-first architecture: data collected on device, synced to cloud when connected; agronomic recommendations generated both offline (cached) and cloud (real-time).
- Use satellite imagery (Sentinel-2, Planet Labs) and ground sensors (soil moisture, temperature, hyperspectral) for plant-level monitoring; data fusion improves prediction.
- Build recommendation engines that respect farmer agency: suggest optimal practices but allow override; a recommendation system that ignores farmer input is ignored.

## Pitfalls
- Assuming broadband connectivity; many farming regions lack reliable internet, so cloud-dependent systems fail.
- Oversimplifying: "plant corn when temp reaches X" ignores soil moisture, frost risk, market conditions — farming is complex optimization.
- Ignoring data ownership; farmers are wary of data sharing; systems must be clear about data handling and give farmers control.

## Tools & references
NOAA weather data, satellite data (Sentinel, Planet, Maxar), IoT sensors (soil, weather), John Deere APIs (tractor telemetry, variable rate), FarmLogs, Gro Intelligence (crop analytics).
