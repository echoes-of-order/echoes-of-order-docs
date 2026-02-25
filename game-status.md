# Current State

**Related docs:** [Architecture](architecture.md) (service layout, authority/simulation) · [Infrastructure](infrastructure.md) (stack, databases, scaling) · [Current Work](current-work.md) (explorations and recent decisions) · [README](README.md) (scope and design focus) · [For Sponsors](sponsor.md)

---

## By the Numbers

| Metric | Value |
|--------|--------|
| TypeScript/TSX lines of code | ~270,000 |
| TypeScript/TSX files | ~3,000 |
| Backend services | 10+ |
| Shared domain packages | 4 (combat engine, movement engine, gRPC contracts, logging) |
| PostgreSQL roles | 5+ (Auth, Global, Realm per realm, Armory, Image-Server) |
| Technology & game-design explorations | 21 |
| Sequence diagrams | 11 |
| Documented decisions | 2 |

Numbers are generated from the project repository (codebase and this documentation). **This section is the single source for these metrics** — other docs link here. One-page summary: [For Sponsors](sponsor.md). The codebase is not public. For milestones and timeline, see [Current Work](current-work.md#milestones).

---

## What Exists

**Infrastructure**

- Kubernetes deployment (Helm charts, k3s for local dev). See [Infrastructure](infrastructure.md#stack) and [Infrastructure](infrastructure.md#realm-isolation).
- Traefik ingress, TLS, service routing
- Separate PostgreSQL instances: auth, global, realm, armory, image-server. See [Infrastructure](infrastructure.md#database-layout).
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

Service roles and data flow are described in [Architecture](architecture.md#service-layout) and [Architecture](architecture.md#communication).

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

For what is currently being explored (Event Bus, Zone Architecture, Event Sourcing, Zero Trust, etc.), see [Current Work](current-work.md). For sequence diagrams (login, reconnect, layers), see [Diagrams](diagrams.md).
