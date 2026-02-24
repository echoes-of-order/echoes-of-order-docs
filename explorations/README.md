# Explorations

Public summaries of technology and game-design explorations. Each document here describes the **problem or idea**, **points considered**, and **outcome** (under evaluation, accepted, on hold, or rejected). Summary and status are in [Current Work](../current-work.md).

**Related docs:** [Current Work](../current-work.md) · [Architecture](../architecture.md) · [Infrastructure](../infrastructure.md)

All documents in this folder are in **English** and written for a public audience (no internal details).

---

## Relationship to internal explorations

**What you see here** are short, distilled summaries: a few paragraphs per exploration, suitable for sponsors and external readers.

**Internally I do not work from these short documents.** I keep full exploration documents in the main repository (under `docs/4_explorations` and related structure). Those internal documents are long-form: they contain detailed analysis, technology comparisons, architecture sketches, code or config examples, trade-off tables, and step-by-step reasoning. They are the source of truth for decisions and implementation.

This folder is a **derived view**: I extract problem, points considered, and outcome from the internal write-ups and publish only that summary here. So: internal = full documentation; this site = brief, public-facing overview. If you need the full context or rationale, that lives in the internal docs, not in these abbreviated pages.

---

## Active — Technology

| Document | Topic |
|----------|--------|
| [2026-01-event-bus-architecture-exploration](active/technology/2026-01-event-bus-architecture-exploration.md) | Event Bus (NATS/JetStream) for Realm Core, Simulations, Armory |
| [2026-01-world-realm-zone-architecture-exploration](active/technology/2026-01-world-realm-zone-architecture-exploration.md) | World / Realm / Zone architecture (WoW-style) |
| [2026-01-wow-style-zone-architecture-exploration](active/technology/2026-01-wow-style-zone-architecture-exploration.md) | WoW-style zones, transitions, layering, warmup |
| [2026-01-event_sourcing_cqrs_architecture_exploration](active/technology/2026-01-event_sourcing_cqrs_architecture_exploration.md) | Event Sourcing + CQRS |
| [2026-01-zero_trust_architecture_exploration](active/technology/2026-01-zero_trust_architecture_exploration.md) | Zero Trust, mTLS, service mesh |
| [2026-01-service_mesh_istio_linkerd_evaluation](active/technology/2026-01-service_mesh_istio_linkerd_evaluation.md) | Service Mesh (Istio/Linkerd) |
| [2025-01-opentelemetry_distributed_tracing_exploration](active/technology/2025-01-opentelemetry_distributed_tracing_exploration.md) | OpenTelemetry distributed tracing |
| [2026-01-elastic-apm-wiki-pilot](active/technology/2026-01-elastic-apm-wiki-pilot.md) | Elastic APM & Wiki pilot |
| [2026-01-player-count-runtime-telemetry-exploration](active/technology/2026-01-player-count-runtime-telemetry-exploration.md) | Player count runtime telemetry |
| [2026-01-bare-metal-pod-scheduling-strategies](active/technology/2026-01-bare-metal-pod-scheduling-strategies.md) | Bare-metal pod scheduling |
| [2025-01-redis_cluster_advanced_caching_strategy](active/technology/2025-01-redis_cluster_advanced_caching_strategy.md) | Redis cluster advanced caching |
| [2025-01-ssl_tls_certificate_management_rotation](active/technology/2025-01-ssl_tls_certificate_management_rotation.md) | SSL/TLS certificate management |
| [2025-01-ssh_key_management_and_security](active/technology/2025-01-ssh_key_management_and_security.md) | SSH key management & security |
| [2025-01-webassembly_combat_performance_optimization](active/technology/2025-01-webassembly_combat_performance_optimization.md) | WebAssembly combat performance |

## Active — Game Design

| Document | Topic |
|----------|--------|
| [2026-01-exploration-custom-spell-creation-morrowind-inspired](active/game-design/2026-01-exploration-custom-spell-creation-morrowind-inspired.md) | Custom spell creation (Morrowind-inspired) |
| [2026-01-exploration-tutorial-design-mmo-principles-josh-strife-hays](active/game-design/2026-01-exploration-tutorial-design-mmo-principles-josh-strife-hays.md) | Tutorial design (MMO principles) |
| [2026-01-exploration-quest-design-morrowind-inspiration](active/game-design/2026-01-exploration-quest-design-morrowind-inspiration.md) | Quest design (Morrowind-inspired) — also accepted direction |

## Accepted

| Document | Topic |
|----------|--------|
| [2026-01-kubernetes_migration_vs_docker_compose_scaling](accepted/technology/2026-01-kubernetes_migration_vs_docker_compose_scaling.md) | Kubernetes vs. Docker Compose — Kubernetes chosen |
| [2026-01-exploration-quest-design-morrowind-inspiration](accepted/gameplay/2026-01-exploration-quest-design-morrowind-inspiration.md) | Quest design (Morrowind-inspired) — accepted |

## On Hold

| Document | Topic |
|----------|--------|
| [2025-06-automated-api-testing](on-hold/process/2025-06-automated-api-testing.md) | Automated API testing |

## Rejected

| Document | Topic |
|----------|--------|
| [2025-01-graphql-subscriptions-vs-colyseus](rejected/technology/2025-01-graphql-subscriptions-vs-colyseus.md) | GraphQL Subscriptions vs. Colyseus |

See [rejected/README.md](rejected/README.md) for the purpose and format of rejected explorations.
