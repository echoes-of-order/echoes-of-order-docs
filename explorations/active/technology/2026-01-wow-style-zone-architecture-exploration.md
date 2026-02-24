# WoW-Style Zone Architecture

**Status:** Active

## Problem / Idea

Moving from a grid-based or generic world model to true zones with clear boundaries, cities, and instances. I needed a concrete design for zone transitions, layering (multiple copies of a zone for capacity), and warmup (preparing simulations before players arrive).

## Points Considered

- Zone boundaries and how players move between zones; handover between simulations.
- Layering: when and how to spin up or merge layers; player distribution and social density.
- Warmup: pre-initialising simulations and caches so that entry into a zone or instance is smooth.
- Instances (e.g. dungeons): entry/exit flow and how they relate to the open world.
- Operational impact: metrics, scaling triggers, and failure handling.

## Outcome

Under evaluation. The high-level direction (zones, layers, warmup) is agreed; detailed implementation paths and parameters are still being worked out.
