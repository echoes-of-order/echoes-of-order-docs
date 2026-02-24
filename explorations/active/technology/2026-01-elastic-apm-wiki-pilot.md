# Elastic APM and Wiki Pilot

**Status:** Active

## Problem / Idea

I wanted to trial an APM (Application Performance Monitoring) product for tracing and performance insight. A single, well-scoped service (the wiki) was chosen as a pilot before rolling out to the rest of the stack.

## Points Considered

- What APM provides: request traces, latency breakdowns, error tracking.
- Elastic APM vs. other options; integration with existing Elasticsearch/Kibana if present.
- Pilot scope: one service (wiki) to validate setup, overhead, and usefulness.
- Success criteria: usable traces, acceptable overhead, clear path to broader rollout.
- Overlap with OpenTelemetry: whether to standardise on one tracing approach long term.

## Outcome

Under evaluation. The wiki pilot is the intended first step. No decision yet on organisation-wide APM or on Elastic vs. OpenTelemetry-based tracing.
