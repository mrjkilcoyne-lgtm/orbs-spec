# Lua

## Scope
Lua as an embedded/extension language: tables, metatables, coroutines, the C API surface.

## Core principles
- The table is the only data structure: arrays, records, modules, objects — all tables plus conventions.
- Metatables define behavior (__index, __newindex, __call): OOP is a pattern you build, not a feature you get.
- Globals are the default and the danger: `local` everything; a typo creates a global silently.
- 1-based indexing and `#` length semantics (undefined with nil holes) shape all array code.
- Lua is designed to be embedded: the host app defines the world; know your host's API (Neovim, Redis, game engine, OpenResty).

## Apex practices
- Module pattern: return a table from the file; no global namespace pollution.
- Use coroutines for cooperative flows (iterators, async in hosts) — they're cheap and first-class.
- Guard nil aggressively: `t and t.field`, default idiom `x = x or default` (mind false).
- For performance hosts (LuaJIT): keep hot loops allocation-free and JIT-friendly (no NYI functions inside).

## Pitfalls
- nil holes breaking `#t` and ipairs silently.
- Accidental global assignment inside functions.
- Assuming string patterns are regex — Lua patterns are their own smaller dialect.

## Tools & references
Programming in Lua (PiL), luacheck, LuaJIT docs, host-specific API refs.
