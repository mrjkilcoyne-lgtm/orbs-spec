# Realtime & WebSockets

## Scope
Pushing live data: WebSockets, SSE, presence, fan-out, connection state at scale.

## Core principles
- Choose the transport by the shape: SSE for server→client streams (simpler, auto-reconnect, HTTP-native), WebSockets for bidirectional, polling for low-frequency — WebSocket-by-default is over-engineering.
- Connections are state: every open socket pins memory and a route to one server; horizontal scale needs a pub/sub backplane (Redis & co.) so any node can reach any client.
- Reconnection is the main flow, not the edge case: clients drop constantly (mobile, laptops sleeping); resume needs message IDs/cursors so clients catch up rather than miss or duplicate.
- Heartbeats detect the dead: TCP won't tell you promptly; ping/pong with timeouts reaps zombies on both ends and keeps intermediaries from idling out connections.
- The realtime layer transports; it must not become the source of truth — persist first, then fan out (or use the log as the source and tail it).

## Apex practices
- Design the protocol explicitly (message types, versioning, acks) even over WebSockets — raw JSON blobs without a version field calcify instantly.
- Backpressure per connection: bounded send buffers, drop/coalesce strategies for slow consumers (a stuck client must not balloon server memory).
- Authenticate at connect and re-check on sensitive actions; tokens expire mid-connection — plan refresh or graceful re-auth.
- Fan-out through topics/rooms with subscription management, and rate-limit client→server messages like any API.

## Pitfalls
- Sticky-session load balancing as the scaling strategy (works until a node dies with 50k connections).
- Missing catch-up: reconnecting clients silently losing messages sent while offline.
- Broadcasting every change to everyone (fan-out explosion) instead of interest-based subscriptions.

## Tools & references
SSE spec, Socket.IO/ws, Redis pub/sub, managed layers (Ably/Pusher), Phoenix Channels as the reference design.
