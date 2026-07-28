# WebAssembly

## Scope
Wasm as a compilation target in and beyond the browser: when it wins, interop costs, the toolchains.

## Core principles
- Wasm wins on compute-dense, allocation-light workloads (codecs, crypto, physics, image processing) — it is not "faster JavaScript" for DOM apps.
- The boundary is the cost: JS↔Wasm calls and memory copies dominate; batch work, pass numbers/typed arrays, minimize chattiness.
- Linear memory is a sandbox: Wasm sees only its own bytes; capability-based safety is the deployment story (plugins, multitenant).
- Source language determines experience: Rust (mature), C/C++ (Emscripten), Go/TinyGo, AssemblyScript — plus GC-language support arriving via WasmGC.
- WASI + component model extend Wasm beyond browsers: portable, sandboxed server/edge/plugin runtimes.

## Apex practices
- Profile before porting: confirm the hot loop is compute-bound and boundary-crossing is amortizable.
- Use wasm-bindgen/generated bindings rather than hand-written glue; keep the interface coarse-grained.
- Stream-compile (instantiateStreaming) and lazy-load the module; Wasm bytes are cacheable assets.
- Consider Wasm for deterministic sandboxing (user plugins, smart-contract-like execution) even when speed isn't the driver.

## Pitfalls
- Porting business logic and losing to serialization overhead at the boundary.
- Shipping multi-MB modules for a function JS did fine.
- Assuming threads/SIMD everywhere (COOP/COEP headers and feature detection required).

## Tools & references
Rust+wasm-bindgen/wasm-pack, Emscripten, wasmtime (WASI), WebAssembly.org specs, twiggy for size profiling.
