# MCP (Model Context Protocol)

## Scope
The open protocol for connecting LLM applications to external tools, data, and prompts: building MCP servers and clients, transports, and the security model of pluggable capability.

## Core principles
- MCP standardizes the M×N integration problem into M+N: any compliant client (Claude Code, IDEs, desktop apps) can use any compliant server, so a tool built once serves every host — the value is the ecosystem contract, not the wire format.
- The primitives have distinct semantics: tools are model-invoked actions, resources are application-managed context (identified by URI), prompts are user-invoked templates; cramming everything into tools forfeits the host's ability to manage context and UX properly.
- It's JSON-RPC 2.0 over pluggable transports — stdio for local subprocess servers, streamable HTTP for remote — with a capability negotiation handshake; local servers inherit the user's OS privileges, remote servers need real authn (the spec uses OAuth 2.1 for HTTP transports).
- Every MCP server you attach extends the model's attack and failure surface: tool descriptions are injected into the model's context (a malicious server can prompt-inject via its own metadata), so servers must be treated like dependencies — pinned, reviewed, and least-privileged.
- Tool schemas and descriptions are consumed by models, not humans: the same craft as function-calling applies — intent-level operations, tight parameter types, and descriptions that say when to use and when not to.

## Apex practices
- Build servers with the official SDKs (TypeScript/Python) and test with MCP Inspector before wiring into a host; hand-rolled JSON-RPC drifts from the spec on lifecycle and error edge cases.
- Scope each server narrowly (one system, one credential boundary) rather than one mega-server: hosts can enable/disable per-server, and narrow servers make permission review tractable.
- Return compact, model-oriented results and use pagination/filter parameters — an MCP tool that dumps 80KB of JSON per call destroys the host's context budget and gets its server disabled.
- For remote/multi-tenant servers, propagate the end user's identity and authorization to the backing system (token exchange, not a shared service account) so audit and access control survive the protocol hop.

## Pitfalls
- Confused-deputy setups: a server holding broad credentials while any connected model (fed untrusted content) can invoke it — combine with retrieved-content injection and you've built an exfiltration pipeline.
- Assuming server trustworthiness is static: a benign server can update its tool descriptions later ("rug pull"); pin versions and re-review on change, as with any supply-chain risk.
- Exposing a raw internal API 1:1 as MCP tools — 40 CRUD endpoints with cryptic parameters is exactly the anti-pattern that makes tool selection fail.

## Tools & references
modelcontextprotocol.io spec and SDKs, MCP Inspector, Anthropic MCP announcement and docs, JSON-RPC 2.0 spec, OAuth 2.1 draft for remote-server auth.
