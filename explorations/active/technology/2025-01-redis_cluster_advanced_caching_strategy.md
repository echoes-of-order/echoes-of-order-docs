# Redis Cluster and Advanced Caching

**Status:** Active

## Problem / Idea

I explored a multi-level caching strategy and Redis in cluster mode for high availability and scale. Topics included invalidation strategies, consistency with the authoritative database, and operational resilience.

## Points Considered

- Caching layers: what to cache (sessions, static data, hot reads); TTL and invalidation rules.
- Redis cluster: sharding, replication, and failover; impact on client usage and operations.
- Consistency: when caches must be invalidated or updated after writes; trade-offs between freshness and performance.
- Operational aspects: monitoring, capacity, and recovery.

## Outcome

Under evaluation. Redis remains the caching technology of choice; cluster mode and detailed invalidation strategies are still being refined.
