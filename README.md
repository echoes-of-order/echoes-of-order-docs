# Echoes of Order

## What This Project Is

Echoes of Order is a **systems-driven, persistent online world** with a strong focus on
**authority, simulation, and long-term world consistency**.

It is not designed as a fast-paced action game or a content-driven theme park.
Instead, it explores how large-scale game worlds can be built as **distributed systems**
where rules, state, and consequences matter.

The project deliberately prioritizes **architecture and correctness** over early gameplay polish.

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
| [Architecture](architecture.md) | Authority, simulation, realm separation |
| [Infrastructure](infrastructure.md) | Kubernetes, distributed systems, scaling |
| [Current State](game-status.md) | What exists, what does not |
| [Current Work](current-work.md) | Active explorations, recent decisions |
| [About the Developer](about-me.md) | Who builds this, background, transparency |
