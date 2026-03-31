# Explorations

Public summaries of technology and game-design explorations. Each file states the **problem or idea**, **what was weighed**, and **outcome** (active, accepted, on hold, rejected). Rolling status: [Current Work](../current-work.md).

**Related docs:** [Current Work](../current-work.md) · [Devlogs](../devlogs/README.md) · [Architecture](../architecture.md) · [Infrastructure](../infrastructure.md)

All files here are **English**, written for a public audience (no secret internals).

## Relationship to internal explorations

What you read here is **short**: a few paragraphs per topic, enough for sponsors or curious engineers.

The **long** versions live in the main monorepo (`docs/4_explorations` and related paths). Those notebooks hold comparisons, sketches, config fragments, and step-by-step reasoning — they are the **source of truth** when a decision ships.

This directory is a **trimmed export**: I distill problem, considerations, and status from the internal doc. Need the full argument? Open the long-form file in the main monorepo under `docs/4_explorations` — this site stays intentionally short.

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

See [rejected/README.md](rejected/README.md) for why rejected write-ups exist.
