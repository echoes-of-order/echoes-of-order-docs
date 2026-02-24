# Bare-Metal Pod Scheduling

**Status:** Active

## Problem / Idea

For production I may want to pin certain workloads to dedicated nodes (e.g. game servers, databases, or GPU-backed services). I explored how to express that in the orchestrator: node labels, taints, tolerations, and affinity so that pods land on the right hardware.

## Points Considered

- Use cases: dedicated nodes for realm simulations; database affinity; optional GPU nodes for combat or other heavy workloads.
- Mechanisms: node labels and selectors; taints and tolerations; pod affinity/anti-affinity.
- Operational impact: capacity planning, upgrades, and failure handling when nodes are dedicated.
- Trade-offs: flexibility vs. predictability; cost and utilisation.

## Outcome

Under evaluation. Dedicated scheduling is a candidate for production. No final policy or node layout yet.
