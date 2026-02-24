# Infrastructure

**Related docs:** [Architecture](architecture.md) (service layout, realm model, communication) · [Current State](game-status.md) (what is deployed today) · [Current Work](current-work.md) (scaling, Event Bus, observability) · [Diagrams](diagrams.md) (warmup, layer merge, metrics)

---

## Philosophy

Infrastructure is not an afterthought. It is part of the game design.

Echoes of Order runs on Kubernetes because:

- Realms need to scale independently
- Simulations need to be replaceable without downtime
- Failure and recovery must be first-class concerns
- The system must behave correctly under partial failure

## Stack

| Component | Choice | Rationale |
|-----------|--------|-----------|
| Orchestration | Kubernetes (k3s locally) | Pod isolation, scaling, self-healing |
| Package management | Helm | Reproducible, versioned deployments |
| Load balancing | Traefik | Ingress, TLS, routing to services |
| Databases | PostgreSQL per domain | Auth, global templates, realm state — isolated |
| Caching | Redis | Sessions, cache, pub/sub |
| Observability | Prometheus, Grafana, Elasticsearch, Kibana | Metrics, dashboards, logs |

## Database Layout

- **Auth DB** (Master + Replicas): Account lookup, character/item/progress events (Armory). Used by Auth Backend and Armory; see [Architecture](architecture.md#service-layout) for the request flow.
- **Global-DB** (Master + Replicas): World data export, realm/character metadata. Feeds Global-Backend and realm/character index; see [Architecture](architecture.md#realm-model) for what realms share.
- **Realm-DB** (Master + Replicas): Character events, player count, login history, world state, wiki persist + search. One per realm; see [Realm Isolation](#realm-isolation) below.

## Realm Isolation

Each realm gets:

- Dedicated Realm-DB instance (or schema)
- Own Event Bus for pub/sub between Realm Core and Realm Simulation
- Own simulation pods (Zones, Instances, Warmup)
- Own ingress rules if needed

Shared services (Auth, Global, Armory, Wiki) are stateless where possible and scoped by realm ID where not. The logical split between realm-owned and shared is described in [Architecture](architecture.md#realm-model).

## Scaling Model

**Horizontal:** More pods per service. Realm-Gateway, simulations, and workers scale out.

**Realm-based:** Add new realm deployments. Each is independent. No shared realm state.

**Database:** Connection pooling, read replicas for heavy query paths. Per-realm DBs avoid cross-realm contention. For layer merge and warmup-driven scaling, see [Diagrams](diagrams.md) (layer-merge-remove-pod, metrics-warmup-scaling).

## What This Enables

- **Rolling updates:** Zero-downtime deploys. Simulations can be swapped out.
- **Failure recovery:** Pods restart. Realm state persists. Simulations reconnect.
- **Scaling:** Add realms or add pods. The architecture does not change.
- **Observability:** Every service exposes metrics. Logs aggregate. Debugging is possible.

Infrastructure is not "just ops." It is the substrate that makes authority and simulation possible.

## Component Model

The system is built from **shared packages** consumed by multiple services:

- Domain engines (combat, movement) as internal libraries
- Typed gRPC contracts for service boundaries
- Centralized logging for observability
- Shared API client and tooling

This reduces duplication, enforces consistency, and makes it clear which code owns what. For the same component view from an authority/simulation perspective, see [Architecture](architecture.md#extracted-components).
