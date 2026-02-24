# Event Sourcing and CQRS

**Status:** Active

## Problem / Idea

Instead of overwriting state, I explored storing an event history and deriving state from it. Commands would change the world; queries would read from materialised views. Goals: audit trail, cheat detection, and scalable read models for combat, inventory, and progress.

## Points Considered

- Event sourcing: what events to store; schema and retention; replay and rebuild of state.
- CQRS: separating command (write) from query (read) paths; eventual consistency and read-model updates.
- Fit with existing authority/simulation model: who writes events, who consumes them, and how validation works.
- Trade-offs: storage growth, replay cost, complexity of debugging and operations.
- Use cases: combat logs, inventory history, progression, analytics.

## Outcome

Under evaluation. Event sourcing and CQRS are promising for consistency and auditability. No decision yet on scope (full world state vs. selected streams) or implementation timeline.
