# Current Work & Explorations

This document lists what is being actively explored and recently decided. It gives sponsors a transparent view of where effort goes. No timelines — only status and focus.

Explorations follow a structured process: research, analysis, decision (accept/reject/on-hold). **Full exploration write-ups** are in [Explorations](explorations/README.md). Decision records (context, rationale, trade-offs) live in the project repository under `docs/3_decisions`.

**Related docs:** [Architecture](architecture.md) (authority, realm model, service layout) · [Infrastructure](infrastructure.md) (stack, scaling, realm isolation) · [Current State](game-status.md) (what exists today) · [Explorations](explorations/README.md) (full write-ups) · [Diagrams](diagrams.md) (sequence diagrams for flows)

**Status at a glance:** 14 active technology explorations, 2 active game design explorations, 2 accepted (Kubernetes migration, Quest design), 1 on hold (Automated API testing). Rejected explorations: [Explorations → Rejected](explorations/README.md#rejected).

---

## Milestones

- **gRPC Character Service:** decided and implemented (2024-12).
- **Kubernetes migration:** decided and implemented (2026-01).
- **Quest design (Morrowind-inspired):** accepted as design direction (2026-01).

No fixed project start date or release timeline — only a commitment to correctness and transparency. For what we're focusing on next, see [Current Focus](#current-focus) below.

---

## Current Focus

Direction for the next phase (no fixed dates):

- **Event Bus rollout** — NATS/JetStream as messaging backbone for Realm Core and Simulations.
- **Zone Architecture** — WoW-style zones, layering, warmup; implementation of accepted world/realm/zone model.
- **First playable loop** — gameplay on top of the existing authority and simulation foundation, when the above is in place.

Details in the tables below and in [Explorations](explorations/README.md).

---

## Active Technology Explorations

| Exploration | Summary | Focus |
|-------------|---------|-------|
| **Event Bus Architecture** | NATS/JetStream as messaging backbone for Realm Core, Simulations, and Armory. Decouples components; no direct Realm ↔ Simulation communication. | Loose coupling, low latency, optional persistence |
| **World / Realm / Zone Architecture** | WoW-style model: no server meshing. One zone = one simulation per layer. Realm = logical unit of truth; simulations are replaceable. | Stability, social density, operational simplicity |
| **WoW-Style Zone Architecture** | From grid-based to true zone simulations. Zone transitions, cities, instances. Technical implementation paths. | Zone boundaries, layering, warmup |
| **Event Sourcing + CQRS** | Event history instead of state overwrite. Commands vs. queries. Audit trail, cheat detection, scalable read models. | Game-state management, combat/inventory consistency |
| **Zero Trust Architecture** | Continuous validation, device trust, context-based access. Beyond JWT: mTLS, service mesh, certificate rotation. | Security, no implicit trust |
| **Service Mesh (Istio/Linkerd)** | Evaluation for mTLS, traffic management, observability between services. | Zero Trust synergy, request-level security |
| **OpenTelemetry Distributed Tracing** | End-to-end tracing for combat flows, login, world updates. Jaeger integration. | Debugging, latency analysis, anomaly detection |
| **Elastic APM & Wiki Pilot** | APM tracing trial. Wiki as first service to validate the approach. | Observability, pilot before rollout |
| **Player Count Runtime Telemetry** | Player count per realm/simulation as Prometheus metric — not DB or domain state. WoW-style architecture. | Scaling decisions, capacity monitoring |
| **Bare-Metal Pod Scheduling** | Node labeling, taints, tolerations for dedicated gaming servers, PostgreSQL affinity, GPU combat backends. | Production deployment, resource placement |
| **Redis Cluster Advanced Caching** | Multi-level caching, invalidation strategies, cluster HA. | Performance, cache consistency |
| **SSL/TLS Certificate Management** | Rotation, automation, Let's Encrypt integration. | Operations, zero-downtime cert updates |
| **SSH Key Management & Security** | Ed25519, certificate-based SSH, Teleport/Vault patterns. | Infra access, audit, rotation |
| **WebAssembly Combat Performance** | Evaluating WASM for combat resolution performance. | Hot path optimization |

**Context:** Event Bus and Zone Architecture tie directly into [Architecture](architecture.md#communication) (Realm Core ↔ Simulation via pub/sub) and [Infrastructure](infrastructure.md#realm-isolation) (per-realm Event Bus). See [Diagrams](diagrams.md) for sequence flows (world events, layer migration, warmup/scaling). Observability and scaling (OpenTelemetry, Player Count Telemetry, Bare-Metal Scheduling) support the model described in [Infrastructure](infrastructure.md#scaling-model) and [Architecture](architecture.md#service-layout).

---

## Active Game Design Explorations

| Exploration | Summary | Focus |
|-------------|---------|-------|
| **Custom Spell Creation (Morrowind-Inspired)** | Optional ability creation for enthusiasts. Gold for creation, resources for use. Instability risk for strong abilities. | Depth without forcing complexity |
| **Tutorial Design (MMO Principles)** | Josh Strife Hays' four principles. Hidden tutorials, competence over completion. | Onboarding without hand-holding |

**Context:** Game design explorations feed into the target player experience described in the [main README](README.md#player-experience-target-state) and [Project Goals](project.md). Current playable state is summarised in [Current State](game-status.md).

---

## Accepted (Recently Decided)

| Exploration | Outcome |
|-------------|---------|
| **Kubernetes vs. Docker Compose** | Kubernetes chosen. Migration completed. Multi-realm management, scaling, and production-readiness require K8s. |
| **Quest Design (Morrowind-Inspired)** | Accepted as design direction. Story-driven quests, long texts, multiple paths, consequences. Short summaries for action-focused players. Implementation to follow. |

**Context:** Kubernetes migration is reflected in [Infrastructure](infrastructure.md) and [Current State](game-status.md). Quest design aligns with the persistent, consequential world in [README](README.md#core-idea).

---

## On Hold

| Exploration | Reason |
|-------------|--------|
| **Automated API Testing** | Deferred. Other infrastructure work prioritised. |

---

## Rejected

Rejected explorations are listed in [Explorations → Rejected](explorations/README.md#rejected) with full write-ups (reasons and lessons learned). Example: [GraphQL subscriptions vs. Colyseus](explorations/rejected/technology/2025-01-graphql-subscriptions-vs-colyseus.md) (rejected in favour of the current WebSocket/Event Bus approach). The current communication model is described in [Architecture](architecture.md#communication).

---

## Key Past Decisions

| Decision | Outcome | When |
|----------|---------|------|
| **Kubernetes Migration** | k3s, Helm, phased migration. Implemented. | 2026-01 |
| **gRPC for Character Service** | Typed contracts for service-to-service. Implemented. | 2024-12 |

Full decision records (context, rationale, trade-offs) are in the project repository under `docs/3_decisions/`. The Kubernetes migration decision directly underpins [Infrastructure](infrastructure.md); the gRPC decision is reflected in [Architecture](architecture.md#communication) and the service layout.

---

## Format & Process

- **Active:** Under evaluation. No decision yet.
- **Accepted:** Decided in favour. Implementation planned or in progress.
- **On Hold:** Paused. May be revisited later.
- **Rejected:** Explicitly declined with documented reasoning.

New explorations are added as markdown files with frontmatter (description, status, tags). Decisions are documented with context and date.
