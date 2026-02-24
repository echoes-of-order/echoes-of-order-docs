# Zero Trust Architecture

**Status:** Active

## Problem / Idea

Moving beyond “authenticated once, then trusted”: I explored continuous validation, device and context checks, and service-to-service security (e.g. mTLS, certificate rotation) so that no component is trusted by default.

## Points Considered

- Zero trust principles: verify explicitly, least privilege, assume breach; applied to game services and operators.
- Beyond JWT: mTLS for service-to-service calls; certificate lifecycle and rotation.
- Relation to a service mesh: automatic mTLS, traffic policy, observability.
- Operational impact: key and cert management, rollout, and failure modes.
- User-facing auth: how login and session validation interact with zero trust at the service layer.

## Outcome

Under evaluation. Zero trust is a target direction for production. Dependency on a service mesh and certificate management is being explored in parallel; no final architecture yet.
