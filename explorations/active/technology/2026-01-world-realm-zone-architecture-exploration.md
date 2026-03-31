# World / Realm / Zone Architecture

**Status:** Active

## Problem / Idea

I needed a clear model for how the persistent world is split into realms and zones: one source of truth per realm, replaceable simulations per zone or layer, no server meshing. The goal is stability, predictable social density, and simple operations.

## Points Considered

- Realm as the single logical unit of truth: one database and one authority per realm; no shared realm state across instances.
- Zone and layer model: one simulation per zone (or per layer within a zone); simulations can be scaled or replaced without changing realm ownership.
- Comparison with server-meshing and other MMO topologies; trade-offs between complexity, latency, and operational burden.
- How scaling works: adding realms versus adding layers or simulation pods within a realm.

## Outcome

Under evaluation. A WoW-style model (realm = unit of truth, one zone = one simulation per layer, no meshing) is the current direction. Detailed zone boundaries, layering, and warmup behavior are still being explored.
