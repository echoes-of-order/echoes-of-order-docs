# SSH Key Management and Security

**Status:** Active

## Problem / Idea

I explored how to manage SSH access to infrastructure in a secure, auditable way: modern key types, certificate-based SSH where applicable, and patterns (e.g. bastion, jump hosts, or third-party access tools) to reduce long-lived keys and improve rotation.

## Points Considered

- Key types and algorithms (e.g. Ed25519); key storage and distribution.
- Certificate-based SSH: short-lived credentials, central signing, and revocation.
- Third-party or in-house tooling for access, audit logs, and session recording.
- Operational impact: onboarding, rotation, and recovery when keys are compromised or lost.

## Outcome

Under evaluation. Stronger key management and optional certificate-based SSH are the direction. No final tooling or process yet.
