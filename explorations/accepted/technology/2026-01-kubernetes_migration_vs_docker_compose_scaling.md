# Kubernetes vs. Docker Compose — Scaling and Multi-Realm

**Status:** Accepted

## Problem / Idea

I needed to run multiple realms, add or remove them over time, and support zero-downtime updates and self-healing. The question was whether Docker Compose could meet these needs or whether to move to an orchestrator like Kubernetes.

## Points Considered

- Multi-realm requirements: several realms at once; dynamic creation when capacity is tight; no manual editing of config for each new realm.
- Docker Compose: static multi-realm configs work but scaling is manual and often requires restarts; script-based workarounds are brittle and not ideal for production.
- Kubernetes: declarative desired state; scaling and rolling updates; separation of realms as workloads; production-oriented tooling and ecosystem.
- Migration cost: effort to move existing services; operational learning; benefits in reliability, scaling, and observability.
- What I explicitly did not want: automatic “sharding” of a single realm across instances (one realm = one logical world; scaling is by adding realms or layers, not by splitting a realm).

## Outcome

**Accepted.** I chose Kubernetes. Migration has been completed. Multi-realm management, scaling, zero-downtime updates, and production readiness are better served by an orchestrator; Docker Compose remains useful for local development (e.g. with k3s or similar).
