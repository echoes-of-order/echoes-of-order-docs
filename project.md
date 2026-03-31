# Project Goals & Approach

**Related docs:** [README](README.md) · [Architecture](architecture.md) · [Infrastructure](infrastructure.md) · [Current Work](current-work.md)

## What I'm Building Toward

Can a persistent game world be a **distributed system on purpose** — authority explicit, state consistent, infra treated as creative constraint? Echoes of Order is that experiment.

## Design Goals

**Authority first.** The realm owns commits. See [Architecture](architecture.md#authority--simulation) and [Architecture](architecture.md#realm-model).

**Simulation as a service.** Combat, NPC logic, and movement run as workers that **propose** outcomes; authority accepts or rejects. Wiring detail: [Architecture](architecture.md#service-layout), [Architecture](architecture.md#communication).

**Persistence by default.** No soft-reset design philosophy. What happens in a realm stays there unless the **rules** say otherwise.

**Scalability through isolation.** New realms add capacity without rewriting the core. Blast radius stays small.

## How I Got Here

The starting question was crude: *What if the world is closer to a database than a stage?*

That pushed me toward:

- Splitting authority from simulation
- Making realms hard boundaries early
- Standing up Kubernetes, gRPC, and messaging **before** chasing content milestones

The payoff is a tree of services and packages where gameplay can land later without rewriting the substrate.

**Modular construction**

Combat, movement, gRPC contracts, and logging live in **shared packages**; apps consume them instead of duplicating domain math. That keeps the authority boundary legible and testable. Map: [Architecture](architecture.md#extracted-components), [Infrastructure](infrastructure.md#component-model).

## Who This Is For

You might care about this project if you like:

- Distributed consistency problems
- Worlds that outlive a single patch
- Architecture that refuses lazy shortcuts
- Games as **engineering** terrain

If that list fits, you are in the right folder.

## Support

Funding and operating stance (solo, transparent, independent): **[For Sponsors](sponsor.md)**.
