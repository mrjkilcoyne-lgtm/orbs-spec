# HTTP Protocols (HTTP/1.1, HTTP/2, HTTP/3/QUIC)

## Scope
The evolution of HTTP semantics and transports: HTTP/1.1 keep-alive and pipelining, HTTP/2 multiplexing over TCP, HTTP/3 over QUIC.

## Core principles
- HTTP semantics (methods, status codes, headers, caching per RFC 9110/9111) are constant across versions; only the wire mapping changes — design APIs against semantics, tune deployments per transport.
- HTTP/1.1 suffers head-of-line blocking at the request level (one response at a time per connection), which browsers work around with ~6 parallel connections per origin; HTTP/2 multiplexes streams over one TCP connection but a single lost TCP segment stalls all streams (transport-level HOL blocking).
- QUIC (RFC 9000) fixes transport HOL blocking with independent streams over UDP, integrates TLS 1.3 into the handshake (1-RTT, 0-RTT resumption), and survives NAT rebinding/network switching via connection IDs — the reason HTTP/3 wins on mobile and lossy paths.
- HTTP/2 flow control is two-level (connection and stream); a small default connection window (65 KB) throttles high-throughput uploads until the server sends WINDOW_UPDATEs — many "HTTP/2 slower than 1.1" reports trace to this.
- Caching is the biggest performance lever in HTTP: Cache-Control directives, ETag/If-None-Match revalidation, and Vary correctness determine whether your CDN serves 95% or 5% of traffic.

## Apex practices
- Terminate HTTP/2 and HTTP/3 at the edge and speak HTTP/1.1 to backends unless you need gRPC — it isolates protocol complexity where it pays (client RTTs) and keeps backend debugging simple.
- Test HTTP/2-specific attack surface: request smuggling via h2→h1 downgrade (header injection through translation), and stream-reset floods (CVE-2023-44487 Rapid Reset) — set concurrent-stream and reset-rate limits.
- Use `curl -v --http2` / `--http3` and browser DevTools protocol column to confirm which version actually negotiated (ALPN, Alt-Svc); assumptions about "we're on h2" are wrong surprisingly often.
- Exploit 0-RTT carefully: only for idempotent requests, since 0-RTT data is replayable by design.

## Pitfalls
- Sharding assets across domains (an HTTP/1.1 optimization) under HTTP/2/3 — it defeats multiplexing and prioritization, adding connections and handshakes for negative gain.
- Getting Vary wrong: omitting `Vary: Accept-Encoding` or varying on whole Cookie headers either poisons caches or nukes hit rates to zero.
- Assuming UDP is open: some networks block or throttle UDP 443, so HTTP/3 clients must race or fall back to TCP (happy-eyeballs-style); shipping h3-only breaks real users.

## Tools & references
RFC 9110-9114 (HTTP semantics/caching/1.1/2/3), RFC 9000 (QUIC); curl, h2load, Wireshark with TLS keylog, quiche/quic-go interop matrix, web.dev/performance.
