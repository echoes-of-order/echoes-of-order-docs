# Current State

## What Exists

**Infrastructure**

- Kubernetes deployment (Helm charts, k3s for local dev)
- Traefik ingress, TLS, service routing
- Separate PostgreSQL instances: auth, global, realm, armory, image-server
- Redis for sessions and caching

**Services**

- **Auth Backend:** Account lookup, JWT sessions
- **Realm Gateway:** Authenticated routing, server/control panel config
- **Global-Backend:** World data, realm/character metadata, desired state apply to Realm Core
- **Realm Core:** Authority, attach player sessions, gRPC to simulations
- **Realm Simulation:** Zones, Instances, Warmup — non-authoritative, Event Bus
- **World Event Backend (Admin):** gRPC to Realm Core
- **Armory:** Client, Indexer, Backend — character/item/progress events to Auth DB
- **Wiki:** Client, Backend, Documentation Exporter — persist + search via Realm-DB
- **Image-Server:** Media and asset handling
- **Observability:** Elastic/Kibana, Grafana, Prometheus (traces, logs, metrics)

**Architecture**

- gRPC and pub/sub (Event Bus) for Realm Core ↔ Realm Simulation
- Auth DB, Global-DB, Realm-DB (Master + Replicas)
- Kubernetes control plane for desired state apply

**Extracted domain logic**

- Combat resolution engine: damage, stats, equipment, battle mechanics. Used for
  simulation and balance testing.
- Movement and positioning engine: positions, facing, movement patterns. Used by
  combat and world entities.
- Centralized logging with Elasticsearch integration across all services.

## What Does Not Exist (Yet)

**Gameplay**

- No publicly playable game loop
- No polished combat, quests, or progression
- No content designed for player consumption

**Player-Facing**

- Frontend exists but is minimal — tools for development, not a finished game client
- No onboarding, no tutorials, no content pacing

## Honest Assessment

The project is in the **infrastructure and authority** phase.

At present:

- A working multi-service backend exists
- Realm isolation and persistence are in place
- A clear model for authority vs. simulation exists

There is *not* yet:

- A game you can sit down and play
- Content designed for engagement
- Any timeline for when that will change

The goal right now is **correctness and coherence**. Gameplay will build on top of that — when the foundation is ready. No promises beyond that.

For what is currently being explored (Event Bus, Zone Architecture, Event Sourcing, Zero Trust, etc.), see [Current Work](current-work.md).
