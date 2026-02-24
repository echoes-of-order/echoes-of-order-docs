# OpenTelemetry Distributed Tracing

**Status:** Active

## Problem / Idea

I needed end-to-end tracing for critical flows (e.g. login, combat, world updates) to debug latency, find bottlenecks, and detect anomalies. OpenTelemetry was evaluated as a vendor-neutral standard with existing backend integrations.

## Points Considered

- What to trace: login and session attach; combat resolution; world state updates; key service-to-service calls.
- Instrumentation: automatic (e.g. via mesh or SDK) vs. manual; overhead and sampling.
- Backend: Jaeger or similar for storage and visualisation; retention and cost.
- Correlation with logs and metrics; alignment with existing observability stack.
- Relation to other work: service mesh (auto-instrumentation), Elastic APM (alternative or complement).

## Outcome

Under evaluation. Distributed tracing is a target for production. OpenTelemetry is the preferred approach; rollout scope and backend choice are still being decided.
