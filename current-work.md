# Current Work & Explorations

This document lists what is being actively explored and recently decided. It gives sponsors a transparent view of where effort goes. No timelines — only status and focus.

Explorations follow a structured process: research, analysis, decision (accept/reject/on-hold). Full documents live in the project repository under `docs/4_explorations` and `docs/3_decisions`.

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

---

## Active Game Design Explorations

| Exploration | Summary | Focus |
|-------------|---------|-------|
| **Custom Spell Creation (Morrowind-Inspired)** | Optional ability creation for enthusiasts. Gold for creation, resources for use. Instability risk for strong abilities. | Depth without forcing complexity |
| **Tutorial Design (MMO Principles)** | Josh Strife Hays' four principles. Hidden tutorials, competence over completion. | Onboarding without hand-holding |

---

## Accepted (Recently Decided)

| Exploration | Outcome |
|-------------|---------|
| **Kubernetes vs. Docker Compose** | Kubernetes chosen. Migration completed. Multi-realm management, scaling, and production-readiness require K8s. |
| **Quest Design (Morrowind-Inspired)** | Accepted as design direction. Story-driven quests, long texts, multiple paths, consequences. Short summaries for action-focused players. Implementation to follow. |

---

## On Hold

| Exploration | Reason |
|-------------|--------|
| **Automated API Testing** | Deferred. Other infrastructure work prioritised. |

---

## Rejected

Rejected explorations are documented in `docs/4_explorations/rejected/` with reasons and lessons learned. Examples: GraphQL subscriptions vs. Colyseus (rejected in favour of current approach).

---

## Key Past Decisions

| Decision | Outcome | When |
|----------|---------|------|
| **Kubernetes Migration** | k3s, Helm, phased migration. Implemented. | 2026-01 |
| **gRPC for Character Service** | Typed contracts for service-to-service. Implemented. | 2024-12 |

Full decision records (context, rationale, trade-offs) are in `docs/3_decisions/`.

---

## Format & Process

- **Active:** Under evaluation. No decision yet.
- **Accepted:** Decided in favour. Implementation planned or in progress.
- **On Hold:** Paused. May be revisited later.
- **Rejected:** Explicitly declined with documented reasoning.

New explorations are added as markdown files with frontmatter (description, status, tags). Decisions are documented with context and date.
