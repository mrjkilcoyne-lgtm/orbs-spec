# Real-User Monitoring

## Scope
Observability from the end-user perspective: Web Vitals, performance metrics, and error tracking in production browsers.

## Core principles
- Real-user monitoring (RUM) captures what actual users experience: network latency, device capabilities, and resource constraints.
- Web Vitals (LCP, FID, CLS) are Google's recommended metrics for page quality; they correlate with user satisfaction and SEO ranking.
- RUM data is noisy (different devices, networks, geographies) but representative; synthetic tests are clean but unrealistic.
- Sampling is essential; collecting RUM from all users is expensive; 10-50% sampling is typical.
- Resource timing (time to first byte, DNS, TCP) reveals server and network issues; interaction timing reveals JavaScript problems.

## Apex practices
- Instrument Web Vitals (Google Web Vitals library) and send them to a backend for aggregation.
- Use session recording (Hotjar, LogRocket) on sampled sessions to reproduce user issues (but privacy is critical).
- Monitor Core Web Vitals (LCP < 2.5s, FID < 100ms, CLS < 0.1) as KPIs; they affect both UX and SEO.
- Correlate RUM metrics with server-side metrics to find the root cause (is the network slow, or is the server slow?).

## Pitfalls
- Over-instrumentation of RUM that slows down the page (defeating the purpose); keep RUM lightweight (< 50KB).
- Privacy violations from over-aggressive session recording; avoid capturing user input or sensitive data.
- Ignoring geographic distribution; a metric aggregated globally hides regional issues (e.g., users in Asia seeing slow CDN).

## Tools & references
Google Web Vitals library, Datadog Real User Monitoring, New Relic RUM, Hotjar, LogRocket, Sentry (error tracking), Web Vitals API (Chrome DevTools), Resource Timing API, Performance Observer API.
