# Web Performance

## Scope
Loading and runtime performance: Core Web Vitals, the critical path, JS cost.

## Core principles
- Performance is user-experienced milestones (LCP, INP, CLS), not benchmark scores; measure on real devices/networks (field data > lab).
- The critical rendering path: HTML → CSS → render; every blocking script/stylesheet delays first paint.
- JavaScript is the most expensive byte: parse/compile/execute on the main thread; ship less before optimizing what ships.
- Images are the heaviest bytes: right-size, modern formats (AVIF/WebP), lazy-load below the fold, dimensions set (CLS).
- Caching layers compound: CDN, HTTP cache headers, service worker, memory — design them as a hierarchy.

## Apex practices
- Set budgets in CI (bundle size, LCP) — regressions blocked, not discovered in the field.
- Code-split by route, preload what's imminent (fonts with crossorigin, hero image with fetchpriority).
- Hunt long tasks (>50ms) in DevTools Performance; break up with scheduler.yield/idle callbacks or move to workers.
- Use CrUX/RUM data to prioritize: fix the p75 phone user, not your M-series laptop.

## Pitfalls
- Lighthouse-100 on desktop while p75 mobile LCP is 6s.
- Hydration-heavy frameworks shipping the whole app to render a blog post.
- Layout thrash: interleaved reads/writes of layout properties in loops.

## Tools & references
web.dev/vitals, Chrome DevTools Performance panel, WebPageTest, bundle analyzers.
