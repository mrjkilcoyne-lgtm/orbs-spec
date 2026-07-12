# Progressive Web Apps

## Scope
Installable, offline-capable web apps: service workers, manifests, caching strategies.

## Core principles
- The service worker is a programmable network proxy: every fetch can be answered from cache, network, or synthesized — with great power comes cache-invalidation responsibility.
- Offline is a spectrum: cache the shell first, then static assets, then data strategies per resource type.
- Choose caching strategy per resource: cache-first (immutable assets), stale-while-revalidate (most content), network-first (fresh data).
- The SW lifecycle (install → waiting → activate) is where update bugs live: users can be one version behind until all tabs close.
- Installability is a contract: manifest + icons + offline response = OS-level presence, but earn the install prompt with value first.

## Apex practices
- Use Workbox rather than hand-rolling SW logic; precache hashed assets, runtime-cache the rest.
- Design the update UX deliberately: detect waiting worker, prompt "refresh for update," skipWaiting on consent.
- Version caches and delete old ones in activate; test the second load and the offline load in CI.
- Background Sync for resilient writes; queue mutations offline, replay on reconnect.

## Pitfalls
- A stale SW caching the old app forever (the self-inflicted unfixable bug — always plan the escape hatch).
- Caching opaque cross-origin responses until quota kills you.
- Treating the SW as optional plumbing and shipping it untested.

## Tools & references
Workbox, web.dev PWA course, Chrome DevTools Application panel, PWABuilder.
