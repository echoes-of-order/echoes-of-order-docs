# Project Goals & Approach

**Related docs:** [README](README.md) (what the project is, core idea) · [Architecture](architecture.md) (authority, simulation, realm model) · [Infrastructure](infrastructure.md) (scaling, isolation) · [Current Work](current-work.md) (explorations and decisions)

---

## What I'm Building Toward

Echoes of Order aims to demonstrate that large-scale, persistent game worlds can be
architected as **distributed systems** — where authority is explicit, state is consistent,
and the infrastructure itself is part of the design.

## Design Goals

**Authority first.** The realm owns the world. Nothing escapes its validation. See [Architecture](architecture.md#authority--simulation) and [Architecture](architecture.md#realm-model).

**Simulation as a service.** Combat, NPC logic, and movement run as replaceable simulations
that propose outcomes. The authority accepts or rejects them. The service layout and communication (gRPC, Event Bus) are in [Architecture](architecture.md#service-layout) and [Architecture](architecture.md#communication).

**Persistence by default.** There is no "soft reset." What happens in the world stays
in the world.

**Scalability through isolation.** Each realm is independent. New realms can be added
without rewriting the core. Failures are contained.

## How I Got Here

The project started with a question: *What if I treat the game world like a database?*

Not as a stage for scripts, but as a coherent system of state, events, and rules.
That led to:

- Separating authority from simulation
- Designing realms as first-class boundaries
- Building infrastructure (Kubernetes, gRPC, event systems) before content

The result is a codebase focused on **structural integrity** — so that if and when
gameplay and content arrive, they rest on a solid foundation.

**Modular construction**

Domain logic is extracted into reusable packages: combat resolution, movement and
positioning, typed service contracts (gRPC), shared logging. Services consume these
libraries rather than duplicating logic. This keeps the authority boundary clean and
allows each piece to be tested and evolved independently. Details: [Architecture](architecture.md#extracted-components), [Infrastructure](infrastructure.md#component-model).

## Who This Is For

This project is for people who care about:

- Distributed systems and consistency
- Long-lived, persistent worlds
- Architecture that refuses to cut corners
- Games as engineering problems worth solving well

If that resonates, you're in the right place.
