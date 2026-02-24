# Sequence Diagrams & Visuals

This page indexes all sequence diagrams and key visuals used in the documentation. Use them to understand flows in depth; the main docs link here where relevant.

| Diagram | Description | Referenced in |
|--------|-------------|----------------|
| [sequence-login-gameplay-session.svg](images/sequence-login-gameplay-session.svg) | Login to gameplay session: Auth, Gateway, Realm, session attach | [Architecture](architecture.md#service-layout), [Infrastructure](infrastructure.md) |
| [sequence-connection-lost-fallback-layer.svg](images/sequence-connection-lost-fallback-layer.svg) | Client connection lost and fallback layer behaviour | [Architecture](architecture.md#event--state-flow) |
| [sequence-client-reconnect-resync.svg](images/sequence-client-reconnect-resync.svg) | Client reconnect and state resynchronisation | [Architecture](architecture.md#event--state-flow) |
| [sequence-layer-migration.svg](images/sequence-layer-migration.svg) | Layer migration and simulation handover | [Architecture](architecture.md#realm-model), [Current Work](current-work.md) (WoW-Style Zone) |
| [sequence-layer-merge-remove-pod.svg](images/sequence-layer-merge-remove-pod.svg) | Layer merge and simulation pod removal | [Infrastructure](infrastructure.md#scaling-model), [Current Work](current-work.md) |
| [sequence-world-event-eventbus.svg](images/sequence-world-event-eventbus.svg) | World events and Event Bus flow | [Architecture](architecture.md#communication), [Current Work](current-work.md) (Event Bus) |
| [sequence-metrics-warmup-scaling.svg](images/sequence-metrics-warmup-scaling.svg) | Metrics-driven warmup and scaling decisions | [Infrastructure](infrastructure.md#scaling-model), [Current Work](current-work.md) (Player Count Telemetry) |
| [sequence-warmup-configuration-techadmin.svg](images/sequence-warmup-configuration-techadmin.svg) | Tech-Admin warmup configuration flow | [Infrastructure](infrastructure.md#component-model) |
| [sequence-switch-simulation-target.svg](images/sequence-switch-simulation-target.svg) | Switching simulation target (e.g. zone change) | [Architecture](architecture.md#authority--simulation), [Current Work](current-work.md) (Zone Architecture) |
| [sequence-dungeon-instance-entry.svg](images/sequence-dungeon-instance-entry.svg) | Entering a dungeon instance | [Architecture](architecture.md#service-layout), [Current Work](current-work.md) (WoW-Style Zone) |
| [sequence-dungeon-exit-open-world.svg](images/sequence-dungeon-exit-open-world.svg) | Exiting instance back to open world | [Architecture](architecture.md#service-layout) |

For service topology and data flow, see the Mermaid diagrams in [Architecture](architecture.md#service-layout) and [Infrastructure](infrastructure.md#stack).
