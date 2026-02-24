# Player Count Runtime Telemetry

**Status:** Active

## Problem / Idea

I needed a reliable way to know how many players are in each realm (and per zone or layer) for scaling and capacity decisions. The requirement was to treat this as runtime telemetry (e.g. metrics), not as domain state stored in the game database.

## Points Considered

- Source of truth: where player presence is known (e.g. session attach/detach) and how to aggregate it into counts.
- Export: metrics (e.g. Prometheus) per realm and optionally per simulation/layer; no persistent domain model for “current player count”.
- Use: autoscaling, capacity alerts, and operations; alignment with a WoW-style zone/layer model.
- Consistency: eventual consistency of counts vs. strong consistency; impact of failures and reconnects.

## Outcome

Under evaluation. Player count as a metric (not domain state) is the intended direction. Exact schema and implementation are still being defined.
