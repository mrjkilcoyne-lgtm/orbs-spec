# Browser APIs

## Scope
The platform beyond the DOM: storage, workers, observers, network, device APIs.

## Core principles
- The platform ships more than you think: check MDN/caniuse before adding a dependency (URL, Intl, structuredClone, dialog...).
- The main thread is sacred: Web Workers for CPU work, and observers (Intersection/Resize/Mutation) instead of polling.
- Storage has tiers: localStorage (sync, small, string), IndexedDB (async, structured, large), Cache API (requests) — plus eviction rules per origin.
- Permissions-gated APIs (geolocation, notifications, camera) demand progressive enhancement and user-gesture initiation.
- AbortController is the universal cancellation token: fetch, event listeners, streams — wire it through.

## Apex practices
- Feature-detect, never UA-sniff; wrap risky APIs in capability checks with fallbacks.
- Use IntersectionObserver for lazy loading/visibility analytics — it's the 90%-cheaper answer to scroll handlers.
- Streams API for large payloads (process while downloading) instead of buffering everything.
- Broadcast Channel/SharedWorker for cross-tab coordination instead of localStorage-event hacks.

## Pitfalls
- localStorage as a database (sync main-thread JSON parsing of megabytes).
- Event listeners leaked on removed elements/closed connections (use AbortController's signal).
- Assuming APIs exist in workers/iframes/private mode without checking.

## Tools & references
MDN Web APIs index, caniuse.com, web.dev capabilities articles, whatwg specs when precision matters.
