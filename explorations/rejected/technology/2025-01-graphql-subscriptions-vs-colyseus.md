# GraphQL Subscriptions vs. Colyseus (Real-Time Game Features)

**Status:** Rejected

## Problem / Idea

I evaluated whether GraphQL Subscriptions could replace or complement the existing real-time layer (WebSocket-based, with a game-server framework) for in-game features such as live state updates, movement, and combat.

## Points Considered

- GraphQL Subscriptions: real-time over WebSocket, schema-based, good for request/response-style subscriptions; typically JSON.
- Game-server framework (e.g. Colyseus): built for game loops, state sync, rooms, and often binary protocols; optimized for high update rates and many concurrent connections.
- Comparison: bandwidth and update rate; built-in state sync, room management, and lag compensation vs. implementing them on top of GraphQL.
- Fit with the architecture: authoritative server state, high-frequency updates, and predictable latency are required; a game-oriented stack aligned better with that.

## Outcome

**Rejected.** I did not adopt GraphQL Subscriptions for core real-time game features. The game-server approach (WebSocket + binary protocol, built-in state sync and rooms) was a better fit for performance, latency, and development effort. GraphQL remains an option for other API surfaces (e.g. queries and mutations) where real-time push is not the main requirement.
