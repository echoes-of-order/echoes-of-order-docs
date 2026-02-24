# Echoes of Order

**Quick navigation:** [Architecture](architecture.md) · [Infrastructure](infrastructure.md) · [Current State](game-status.md) · [Current Work](current-work.md) · [Diagrams](diagrams.md) · [Project Goals](project.md) · [About](about-me.md)

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

## Status

Echoes of Order is an active, long-term **solo project**. No team. No investors.

The architecture is real. The systems are evolving. The game itself is still becoming.

**No promises** of timelines or features. Only a commitment to correctness, clarity, and transparency. Important decisions are documented and made available.

---

## Documentation

| Document | Content |
|----------|---------|
| [Architecture](architecture.md) | Authority vs. simulation, realm model, service layout, communication (HTTP/gRPC, Event Bus). Start here for how the world is owned and how simulations propose changes. |
| [Infrastructure](infrastructure.md) | Kubernetes (k3s), Helm, Traefik, database layout (Auth/Global/Realm), realm isolation, scaling model. Complements [Architecture](architecture.md) with deployment and operations. |
| [Current State](game-status.md) | What exists today (services, infra, domain engines) and what does not (gameplay, content). Honest assessment of the current phase. |
| [Current Work](current-work.md) | Active technology and game-design explorations, accepted/rejected decisions, links to related docs and to full exploration documents in the project repository. |
| [Diagrams](diagrams.md) | Index of all sequence diagrams (login, reconnect, layer migration, Event Bus, warmup, dungeon flow, etc.) with short descriptions and where they are referenced. |
| [Project Goals](project.md) | Design goals (authority first, simulation as a service, persistence, scalability) and who this project is for. |
| [About the Developer](about-me.md) | Who builds this, background, transparency commitment. |

Full exploration write-ups and decision records (context, rationale, trade-offs) live in the project repository under `docs/4_explorations` and `docs/3_decisions`.
