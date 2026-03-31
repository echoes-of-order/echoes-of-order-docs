# Service Mesh (Istio / Linkerd) Evaluation

**Status:** Active

## Problem / Idea

I evaluated a service mesh to get automatic mTLS between services, traffic management, and better observability. The mesh would sit between the game services and support zero-trust and tracing goals.

## Points Considered

- Features: automatic mTLS, traffic splitting, retries, and observability (metrics, tracing).
- Istio vs. Linkerd: complexity, resource usage, and fit with the stack.
- Prerequisites: Kubernetes as the base; relation to existing ingress and service discovery.
- Operational cost: installation, upgrades, debugging, and failure behavior.
- Overlap with other explorations: zero trust (mTLS), OpenTelemetry (tracing), Kubernetes migration.

## Outcome

Under evaluation. A service mesh is a candidate for production. Technology choice (Istio vs. Linkerd) and rollout plan are not yet decided.
