# SSL/TLS Certificate Management and Rotation

**Status:** Active

## Problem / Idea

I needed a clear approach to obtaining, deploying, and rotating TLS certificates for ingress and services so that HTTPS can run with minimal downtime and manual work. Automation (e.g. with a public CA) and zero-downtime rotation were goals.

## Points Considered

- Certificate sources: public CA (e.g. Let’s Encrypt) vs. internal CA; automation and renewal.
- Storage and distribution: where certs live and how they are pushed to ingress or services.
- Rotation: how to roll out new certs without dropping connections; integration with the ingress layer.
- Operational practices: monitoring expiry, renewal failures, and rollback.

## Outcome

Under evaluation. Automated issuance and rotation are the target. Tooling and exact workflow are still being decided.
