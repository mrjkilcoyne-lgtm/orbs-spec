# Elixir

## Scope
Elixir on the BEAM: processes, OTP, fault tolerance, Phoenix.

## Core principles
- Processes are the unit of everything: isolation, concurrency, state, failure — millions of them are normal.
- Let it crash: don't defensively code every failure; supervisors restart from a known-good state.
- Immutable data + message passing removes data-race classes entirely.
- Pattern matching in function heads is the control flow: match on shapes, not if-trees.
- OTP behaviors (GenServer, Supervisor) are proven skeletons — reach for them before hand-rolling process loops.

## Apex practices
- Design the supervision tree first: what restarts together, in what order, with what strategy.
- Keep GenServer callbacks fast; move heavy work to Task/queues so mailboxes don't back up.
- Use `with` for happy-path pipelines over nested case; tagged tuples ({:ok, _}/{:error, _}) everywhere.
- Telemetry + observability from day one; the BEAM exposes everything (observer, :recon).

## Pitfalls
- Storing giant state in one GenServer, creating a bottleneck singleton.
- Sending huge messages between processes (copied, not shared).
- Using processes for code organization instead of runtime concerns — modules organize code, processes organize failure/concurrency.

## Tools & references
Elixir guides, "Designing Elixir Systems with OTP", Phoenix/LiveView docs, credo, dialyzer.
