# Offline-Sync

## Scope
Making apps work offline: local persistence, eventual consistency, conflict resolution, and sync strategies.

## Core principles
- Local-first architecture: write to local DB first, sync to server asynchronously — enables offline UX and resilience to network outages.
- Conflict resolution occurs when the app tries to sync a local change that conflicts with a server change (last-write-wins, application-specific logic, or manual merge).
- Vector clocks or lamport clocks track causality; without them, determining which version is "newer" is ambiguous (both sides claim last-write-wins).
- Eventual consistency: after a network partition heals, all clients eventually see the same state — accept temporary divergence and use CRDTs or application logic for automatic resolution.
- CRDTs (Conflict-free Replicated Data Types) like LWWRegister, Counter, or Set merge divergent updates automatically without coordination.

## Apex practices
- Use Room (Android) or Core Data / Realm (iOS) for local persistence; include sync metadata (server version, local dirty flag).
- Sync strategy: pull on launch, push mutations immediately, and pull periodically (exponential backoff if failed); handle 409/conflict responses with merge logic.
- Use a sync queue: store pending mutations locally, replay them if sync fails, deduplicate by client-generated ID.
- Test with network simulation: Airplane Mode, slow 3G, packet loss; ensure the app degrades gracefully (local reads work, mutations queue).

## Pitfalls
- Two-way sync without conflict resolution; two clients modify the same field offline, sync order determines winner — define behavior explicitly.
- Timestamp-based resolution (server time wins) across devices with clock drift — use version numbers or logical clocks instead.
- Ignoring data consistency: a user changes data locally, sees it, then close and reopen the app to find server version (sync failed silently).

## Tools & references
CRDT data structures, Replicache (sync framework), Room + WorkManager, Core Data + CloudKit, Firebase Realtime Database; "Designing Data-Intensive Applications" (Kleppmann) chapters on consistency.
