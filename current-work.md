# Current Work & Explorations

Snapshot of **active and recent** technology and design threads. Intent: sponsors and engineers see **where time goes** without pretending there is a fixed shipping calendar.

Process: research → write-up → accept, reject, or park. Longer public summaries: [Explorations](explorations/README.md). Shipped narratives: [Devlogs](devlogs/README.md). Formal decision context: main repo `docs/3_decisions`.

**Related docs:** [Architecture](architecture.md) · [Infrastructure](infrastructure.md) · [Current State](game-status.md) · [Explorations](explorations/README.md) · [Devlogs](devlogs/README.md) · [Diagrams](diagrams.md)

**At a glance:** 14 active technology explorations, 2 active game-design threads, 2 accepted directions (Kubernetes path, quest design), 1 on hold (automated API testing). Rejected list: [Explorations → Rejected](explorations/README.md#rejected).

## Milestones

- **gRPC Character Service:** shipped (2024-12).
- **Kubernetes migration:** shipped (2026-01).
- **Quest design (Morrowind-inspired):** accepted direction (2026-01).
- **Envoy Gateway + Gateway API:** edge HTTPS routing shipped; Traefik/Ingress retired (2026-03). [Devlog #2](devlogs/2026-03-devlog-02-traefik-envoy-gateway-migration.md).
- **SSO web app + PKCE:** central login surface and authorization code flow for clients (2026-03). [Devlog #3](devlogs/2026-03-devlog-03-sso-pkce-migration.md).

No public “we launch on …” dates — see [Current Focus](#current-focus) for emphasis.

## Current Focus

Next emphasis (unordered, **no** promised dates):

- **Event Bus** — NATS/JetStream between Realm Core and simulations.
- **Zone architecture** — WoW-style zones, layering, warmup on top of the accepted world/realm model.
- **First playable loop** — only after the two above settle on production-shaped wiring.

Tables below + [Explorations](explorations/README.md) carry detail.

## Active Technology Explorations

| Exploration | Summary | Focus |
|-------------|---------|-------|
| **Event Bus Architecture** | NATS/JetStream backbone for Realm Core, Simulations, Armory. Decouples components; no direct Realm ↔ Simulation calls. | Loose coupling, low latency, optional persistence |
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

**Context:** Event Bus + zone work tie to [Architecture](architecture.md#communication) and [Infrastructure](infrastructure.md#realm-isolation). Sequences: [Diagrams](diagrams.md) (world events, layer migration, warmup). Observability rows align with [Infrastructure](infrastructure.md#scaling-model) and [Architecture](architecture.md#service-layout).

## Active Game Design Explorations

| Exploration | Summary | Focus |
|-------------|---------|-------|
| **Custom Spell Creation (Morrowind-Inspired)** | Optional ability creation for enthusiasts. Gold for creation, resources for use. Instability risk for strong abilities. | Depth without forcing complexity |
| **Tutorial Design (MMO Principles)** | Josh Strife Hays' four principles. Hidden tutorials, competence over completion. | Onboarding without hand-holding |

**Context:** Targets player experience sketched in [README](README.md#player-experience-target-state) and [Project Goals](project.md). Honest “what runs today”: [Current State](game-status.md).

## Accepted (Recently Decided)

| Exploration | Outcome |
|-------------|---------|
| **Kubernetes vs. Docker Compose** | Kubernetes chosen; migration done. Multi-realm ops and scaling drove the call. |
| **Quest Design (Morrowind-Inspired)** | Accepted as design direction. Long text, branching, consequences; short summaries for players who skip lore. Implementation TBD. |

**Context:** Infra reality: [Infrastructure](infrastructure.md), [Current State](game-status.md). Quest stance matches persistence framing in [README](README.md#core-idea).

## On Hold

| Exploration | Reason |
|-------------|--------|
| **Automated API Testing** | Deferred while other infrastructure work stayed hotter. |

## Rejected

[Index + rationale](explorations/README.md#rejected). Example: [GraphQL subscriptions vs. Colyseus](explorations/rejected/technology/2025-01-graphql-subscriptions-vs-colyseus.md) (WebSocket/Event Bus model won). Live communication picture: [Architecture](architecture.md#communication).

## Key Past Decisions

| Decision | Outcome | When |
|----------|---------|------|
| **Envoy Gateway / Gateway API** | Edge ingress; HTTPRoutes; cert-manager TLS. Done. | 2026-03 |
| **Kubernetes Migration** | k3s, Helm, phased cutover. Done. | 2026-01 |
| **gRPC for Character Service** | Typed service contracts. Done. | 2024-12 |

ADR-style depth: `docs/3_decisions/` in the main repository. k8s choice backs [Infrastructure](infrastructure.md); gRPC shows up in [Architecture](architecture.md#communication).

## Format & Process

- **Active:** Still evaluating.
- **Accepted:** Direction chosen; implementation ongoing or planned.
- **On Hold:** Intentionally paused.
- **Rejected:** Documented no with reasons.

New files here use frontmatter (description, status, tags) when mirrored from internal explorations.
