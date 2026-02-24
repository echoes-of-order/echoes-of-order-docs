# WebAssembly for Combat Performance

**Status:** Active

## Problem / Idea

Combat resolution runs on a hot path and must be fast and deterministic. I evaluated whether compiling the combat engine or parts of it to WebAssembly could improve performance (e.g. in a Node or browser context) while keeping the same logic.

## Points Considered

- Where WASM could run: server-side (Node or dedicated runtime) vs. client; impact on authority (server remains authoritative).
- Performance: throughput and latency of WASM vs. current implementation; cost of crossing JS/WASM boundary.
- Determinism: ensuring identical results across runs; testing and replay.
- Trade-offs: build and debugging complexity; maintainability; benefit vs. effort.

## Outcome

Under evaluation. WASM is a possible optimisation. No decision yet on adoption or scope.
