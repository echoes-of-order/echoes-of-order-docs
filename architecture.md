# Architecture

**Related docs:** [Infrastructure](infrastructure.md) (deployment, databases, scaling) · [Current State](game-status.md) (implemented services) · [Current Work](current-work.md) (Event Bus, zone architecture) · [Diagrams](diagrams.md) (sequence diagrams for login, reconnect, layers, Event Bus)

---

## Authority & Simulation

The architecture is built around a clear separation:

**Realm Authority** owns the world state. It is the source of truth. Nothing is committed
without its validation.

**Simulations** propose changes. They run combat, NPC behavior, movement — but they do not
own state. They can be stopped, restarted, or replaced. The authority decides what sticks.

```mermaid
flowchart TB
    authority[Realm Authority<br/>single source of truth per realm]
    authority -->|validates| combat[Combat Simulation]
    authority -->|validates| movement[Movement Simulation]
    authority -->|validates| npc[NPC Behavior Simulation]
    subgraph sims[non-authoritative, can be replaced at any time]
        combat
        movement
        npc
    end
```

## Realm Model

Each realm is an **isolated, authoritative instance** of the game world.

- Own PostgreSQL database
- Own event stream
- Own simulation workers
- No cross-realm state (by design)

Realms share only:

- Account and authentication (Auth-Backend)
- Static templates: items, classes, NPC definitions (Global-Backend, Armory-Backend)
- Asset delivery (Image-Server)

The corresponding database and deployment layout (Auth DB, Global-DB, Realm-DB per realm) is described in [Infrastructure](infrastructure.md#database-layout) and [Infrastructure](infrastructure.md#realm-isolation).

This isolation enables:

- Horizontal scaling (add realms)
- Fault containment (one realm's failure does not cascade)
- Clean boundaries for testing and deployment

## Service Layout

**Main flow: Ingress → Clients → Auth → Realm Gateway → Global-Backend → Realm Core**

```mermaid
flowchart TB
    subgraph ingress[Ingress Layer]
        ing[Ingress Controller]
    end
    subgraph clients[Client Layer]
        web[Web Application]
        admin[Admin UI]
        tech[Tech-Admin UI]
    end
    subgraph auth[Auth Layer]
        authb[Auth Backend]
    end
    subgraph gateway[Gateway Layer]
        rgw[Realm Gateway]
    end
    subgraph meta[Meta Layer]
        gb[Global-Backend]
    end
    subgraph realm[Realm Control]
        rc[Realm Core]
    end
    subgraph dbs[Databases]
        authdb[(Auth DB)]
        globaldb[(Global-DB)]
    end

    ing --> web
    ing --> admin
    ing --> tech
    web --> authb
    admin --> authb
    tech --> authb
    authb -->|account lookup| authdb
    authb -->|authenticated requests| rgw
    rgw --> gb
    gb -->|world data, realm/character metadata| globaldb
    gb -->|desired state apply| rc
```

**Realm Core, Event Bus, and Simulations**

```mermaid
flowchart TB
    subgraph realm[Realm Core]
        rc[Realm Core]
    end
    subgraph bus[Event Bus]
        eb[pub/sub]
    end
    subgraph sims[Realm Simulation]
        zones[Realm Simulation - Zones]
        instances[Realm Simulation - Instances]
        warmup[Warmup Simulations]
    end
    subgraph dbs[Realm DB]
        realmd[(Realm-DB Master + Replicas)]
    end
    weba[World Event Backend Admin]

    rc <-->|gRPC| weba
    rc <-->|gRPC| sims
    rc <-->|pub/sub| eb
    eb <-->|pub/sub| sims
    sims -->|character/item/progress events| realmd
    sims -->|persist world state| realmd
```

**Armory, Wiki, and Observability**

```mermaid
flowchart TB
    subgraph armory[Armory]
        ac[Armory Client]
        ai[Armory Indexer]
        ab[Armory Backend]
    end
    subgraph wiki[Wiki]
        wc[Wiki Client]
        wb[Wiki Backend]
        de[Documentation Exporter]
    end
    subgraph obs[Observability Stack]
        elk[Elastic / Kibana]
        grafana[Grafana]
        prom[Prometheus]
    end
    authdb[(Auth DB)]
    realmd[(Realm-DB)]

    ac --> ai
    ac --> ab
    ai --> ab
    ab -->|character/item/progress events| authdb

    wc --> wb
    wb --> de
    wb -->|persist + search| realmd

    elk --> traces[Traces]
    grafana --> logs[Logs]
    prom --> metrics[Metrics]
```

## Communication

- **Synchronous (HTTP/gRPC):** Service-to-service calls. Auth, Realm Gateway, Global-Backend, Realm Core, World Event Backend. See [Current Work](current-work.md) for gRPC Character Service decision and Event Bus exploration.
- **Persistence (SQL):** Auth DB, Global-DB, Realm-DB. Account lookup, world data, character/item/progress events. See [Infrastructure](infrastructure.md#database-layout).
- **Pub/sub (Event Bus):** Realm Core ↔ Realm Simulation. gRPC messages, world state, desired state apply. Event Bus flow is illustrated in [Diagrams](diagrams.md) (sequence-world-event-eventbus).

## Event & State Flow

1. Player action → Gateway (validated) → Realm
2. Realm delegates to appropriate simulation
3. Simulation proposes result → Authority validates → State updated
4. Relevant clients receive updates via WebSocket

The authority never trusts simulation output blindly. It applies rules, checks constraints,
and only then commits. For sequence-level detail (login, reconnect, layer migration, dungeon entry/exit), see [Diagrams](diagrams.md).

## Extracted Components

The project is structured as a **monorepo with shared libraries**. Domain logic that must
be consistent across services lives in separate packages, published internally and
consumed where needed.

**Domain engines**

- A **combat resolution engine**: Hit/miss/crit, damage calculations, stats, equipment.
  Built for determinism and testability. Used by the global backend for battle simulation
  and balance testing.
- A **movement and positioning engine**: Position, facing, movement patterns, range checks.
  Domain-driven design. Used by combat (position in battle) and world entities (NPC/character
  placement).

These engines are **non-authoritative**. They compute outcomes; the realm authority
validates and commits them.

**Shared communication layer**

- Protocol Buffers and gRPC bindings for service-to-service calls: character data, stats,
  inventory, auras, chat, realm snapshots, simulation events. Strong typing, versioned
  contracts.

**Shared observability**

- A logging library with ECS (Elastic Common Schema) format and Elasticsearch integration.
  Used across all backend services for structured, searchable logs.

**Shared tooling**

- TypeScript API client for frontend and admin. Shared ESLint and code quality config
  across the monorepo.

This structure keeps the authority/simulation boundary clear while allowing domain logic
to evolve independently and be tested in isolation. The same stack (Helm, per-realm resources, shared packages) is described from an operations perspective in [Infrastructure](infrastructure.md#component-model).
