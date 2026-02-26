# Echoes of Order

![Echoes of Order](images/1290x640.jpg)

A **systems-driven, persistent online world** — authority, simulation, and long-term consistency first.

**Quick navigation:** [Architecture](architecture.md) · [Infrastructure](infrastructure.md) · [Current State](game-status.md) · [Current Work](current-work.md) · [Explorations](explorations/README.md) · [Diagrams](diagrams.md) · [Project Goals](project.md) · [About](about-me.md) · [For Sponsors](sponsor.md)

---

## Who This Documentation Is For

This documentation is written for **sponsors, technical readers, and anyone** who wants a clear view of what Echoes of Order is, how it is built, and where the project stands. No marketing fluff — decisions, trade-offs, and current state are documented so that reasoning is traceable and transparent.

---

## How to Read This Documentation

- **New to the project?** Start with this README, then [Architecture](architecture.md) (how the world is owned and how simulations work), then [Current State](game-status.md) (what exists today).
- **Interested in operations and deployment?** [Infrastructure](infrastructure.md) and [Diagrams](diagrams.md) (sequence flows).
- **Want to see what’s being explored or decided?** [Current Work](current-work.md). Full exploration write-ups are in [Explorations](explorations/README.md). Decision records (context, rationale) live in the project repository under `docs/3_decisions`.

---

## What This Project Is

Echoes of Order is a **systems-driven, persistent online world** with a strong focus on
**authority, simulation, and long-term world consistency**.

It is not designed as a fast-paced action game or a content-driven theme park.
Instead, it explores how large-scale game worlds can be built as **distributed systems**
where rules, state, and consequences matter.

The project deliberately prioritizes **architecture and correctness** over early gameplay polish.

---

## What Kind of Game Is Echoes of Order?

**Genre & format.** Echoes of Order is a **persistent online world** in the tradition of MMO-style games: you play as one or more **persistent characters** in a shared, living world. It is **systems-driven**, not a story-led single-player RPG or a content treadmill. The world is built from rules, state, and simulation — not from scripted set pieces.

**How it is meant to be played.** You inhabit a realm with your character. Actions — combat, exploration, interaction with NPCs and systems — have **lasting effects**. The world does not reset for you; it keeps a consistent history. Progression is intended to feel **emergent**: outcomes arise from how you interact with the world and its systems, not from following a fixed quest line. The focus is on a world that **reacts and persists**, not on short sessions or disposable content.

**Atmosphere & tone.** The game aims for a **coherent, consequential world**: a place that exists with its own logic and history. In atmosphere and tone it is intended to sit in the same space as **World of Warcraft** — a living fantasy world that feels consistent, explorable, and consequential. The tone is oriented toward weight and continuity — what you do matters to the world state and to your character over time. It is not a fast-paced arcade experience or a casual drop-in game; it is built for players who want to exist in a world that **remembers** and where **structure and consistency** are part of the experience.

---

## Core Idea

The world of Echoes of Order is persistent.

Actions taken by players, NPCs, and systems are not reset, instanced away, or discarded.
They become part of the world's history and influence future states.

The game is built around three central ideas:

- **Authoritative world state**
- **Deterministic simulation**
- **Consequences that persist beyond a single session**

---

## World & Persistence

The world is divided into **realms**.

Each realm represents a fully authoritative instance of the game world with its own
history, data, and state.

Within a realm:

- NPCs persist
- World events leave traces
- Systems evolve over time
- Players interact with the same underlying world state

There is no concept of a "reset" world.

---

## Simulation Model

Gameplay is driven by **non-authoritative simulations**.

Simulations are responsible for:

- Combat resolution
- NPC behavior
- Movement and interactions
- Localized world logic

However:

- Simulations never own the world state
- Simulations can be stopped or replaced at any time
- All final decisions are validated by the realm authority

This separation allows the world to remain consistent even under failure or scaling events.

---

## Player Experience (Target State)

Players inhabit the world as persistent characters.

The game is designed so that:

- Actions have lasting effects
- Systems react to player behavior
- The world does not exist purely for the player's convenience

Progression is intended to be:

- Systemic, not scripted
- Emergent, not pre-authored
- Shaped by interaction rather than checklists

---

## Scope & Current State

At present:

- The project focuses on **backend, world authority, and simulation architecture**
- Core systems for realms, simulations, events, and persistence exist
- The game is **not yet publicly playable**
- Visuals, content, and player-facing features are secondary at this stage

**By the numbers:** [Current State](game-status.md#by-the-numbers).

---

## What This Game Is Not

Echoes of Order is intentionally **not**:

- A theme-park MMO
- A fast-reset seasonal game
- A short-session arcade experience
- A prototype optimized for quick content delivery

The project explores a different design space:
**long-lived systems, slow change, and structural integrity**.

---

## Why Build a Game Like This?

Many games hide complexity behind scripts and resets.

Echoes of Order explores what happens when:

- The world is treated as a system, not a stage
- Infrastructure is part of game design
- Failure, recovery, and scale are first-class concerns

The goal is not to be bigger — but to be **coherent**.

---

## Why Support Echoes of Order?

This project is **authority-first, transparent, and independent**: decisions and explorations are published, there are no investors or deadlines pushing shortcuts, and the work is documented so it stays useful over time. If you want to support that direction, see [For Sponsors](sponsor.md) for how to contribute and what your support enables.

---

## Status

Echoes of Order is an active, long-term **solo project**. No team. No investors.

The architecture is real. The systems are evolving. The game itself is still becoming.

**No promises** of timelines or features. Only a commitment to correctness, clarity, and transparency. Important decisions are documented and made available.

**Support this work:** [For Sponsors](sponsor.md). **Follow updates:** [Current Work](current-work.md) and [Explorations](explorations/README.md); social and community links: [For Sponsors](sponsor.md#how-to-follow-updates).

---

## Documentation

| Document | Content |
|----------|---------|
| [Architecture](architecture.md) | Authority vs. simulation, realm model, service layout, communication (HTTP/gRPC, Event Bus). Start here for how the world is owned and how simulations propose changes. |
| [Infrastructure](infrastructure.md) | Kubernetes (k3s), Helm, Traefik, database layout (Auth/Global/Realm), realm isolation, scaling model. Complements [Architecture](architecture.md) with deployment and operations. |
| [Current State](game-status.md) | What exists today (services, infra, domain engines) and what does not (gameplay, content). Honest assessment of the current phase. |
| [Current Work](current-work.md) | Active technology and game-design explorations, accepted/rejected decisions, status at a glance. Links to related docs and to full write-ups. |
| [Explorations](explorations/README.md) | Full exploration documents (active, accepted, on-hold, rejected). One document per exploration; all in English. |
| [Diagrams](diagrams.md) | Index of all sequence diagrams (login, reconnect, layer migration, Event Bus, warmup, dungeon flow, etc.) with short descriptions and where they are referenced. |
| [Project Goals](project.md) | Design goals (authority first, simulation as a service, persistence, scalability) and who this project is for. |
| [About the Developer](about-me.md) | Who builds this, background, transparency commitment. |
| [For Sponsors](sponsor.md) | One-page summary: numbers, why support, how to support, how to follow. |

Full exploration write-ups are in [Explorations](explorations/README.md). Decision records (context, rationale, trade-offs) live in the project repository under `docs/3_decisions`.

*Maintainability:* Metrics and "what exists" only in [Current State](game-status.md). Milestones only in [Current Work](current-work.md). Support and community links only in [For Sponsors](sponsor.md). Profile/developer links only in [About the Developer](about-me.md). Update those files to avoid duplication.

---

## Key Terms

| Term | Meaning |
|------|--------|
| **Realm** | An isolated, authoritative instance of the game world with its own database, event stream, and simulation workers. No cross-realm state. |
| **Authority / Realm Authority** | The single source of truth per realm. Validates all changes; simulations propose, authority commits. |
| **Simulation** | Non-authoritative service that runs combat, NPC behavior, movement, or local world logic. Replaceable at any time; never owns state. |
| **Event Bus** | Pub/sub messaging (e.g. NATS/JetStream) between Realm Core and Realm Simulations. No direct Realm ↔ Simulation calls. |
| **Layer** | A logical shard of a zone (e.g. to cap players per instance). One simulation per layer; layers can be merged or scaled. |
| **Realm Core** | The service that embodies realm authority: attaches sessions, talks to simulations via gRPC and Event Bus, persists state. |
| **Realm Gateway** | Entry point for clients: authenticates, routes to the correct realm, exposes WebSocket for gameplay. |
