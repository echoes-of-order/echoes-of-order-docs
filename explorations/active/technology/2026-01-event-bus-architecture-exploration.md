# Event Bus Architecture

**Status:** Active

## Problem / Idea

The game architecture separates a central authority (realm) from replaceable simulations (combat, movement, NPCs). These components must not talk to each other directly. I needed a messaging backbone that keeps them loosely coupled, supports very low latency and many small messages, and allows optional persistence for read models (e.g. character progress).

## Points Considered

- Requirements: no direct authority ↔ simulation communication; loose coupling; low latency; simple topic structure; minimal operational complexity; optional persistent streams for character/progress events.
- Technology: compared dedicated message brokers (e.g. pub/sub with optional streaming) against embedding messaging inside the authority. Evaluated complexity, latency, and operational cost.
- Subject design: how to structure topics for world events (authority → simulations), simulation reports (simulations → authority), and character/progress events (simulations → read-model consumers).
- Persistence: which streams need to be stored for replay, analytics, or read models versus fire-and-forget.
- Operational model: running the bus as shared infrastructure, independent of individual realms.

## Outcome

Under evaluation. A dedicated event bus (pub/sub with optional persistent streams) is the preferred direction. Technology choice and exact subject layout are still being refined. No final implementation decision yet.
