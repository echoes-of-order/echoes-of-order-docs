# Devlog #1 – March 2026

## What this is about

Traefik is out, Envoy Gateway is in. Short version: I moved the cluster from “whatever k3s ships by default” to **Envoy Gateway + Gateway API**, because Ingress was starting to smell like technical debt.

---

## Why Traefik had to go

Traefik came with k3s and worked fine — until the cracks showed. Classic **Ingress** is limited: no header or query matching, no HTTP method matching, no first-class gRPC routing. Traefik *can* speak Gateway API, but we were on plain Ingress only — a spec that’s clearly showing its age.

Then there was **annotation soup**. Traefik annotations here, an nginx one there because tech-admin needed something Traefik couldn’t express cleanly. CRDs/IngressRoute-ish stuff next to plain Ingress. No single mental model. The Traefik dashboard also wasn’t something I’d expose in production. Backend gRPC stayed **inside** the cluster and never hit ingress; anything external and gRPC-shaped would have been a workaround pile later.

So the real question wasn’t “does Traefik work?” — it does. It was **what base do I want five years from now?** Gateway API is Ingress’s successor. Investing there beats polishing legacy Ingress.

---

## Why Envoy Gateway

Traefik wins on **simplicity** and a built-in dashboard everyone knows. Envoy Gateway doesn’t ship a Traefik-style UI — mostly an ops-facing admin view. What it *does* give you is **Gateway API as the only configuration surface**. No hybrid Ingress + annotations, no nginx hacks on a Traefik controller. One YAML shape. **GRPCRoute** for gRPC when you need it. Envoy underneath — same data plane family as Istio, battle-tested, CNCF reference implementation for Gateway API.

Trade-off: steeper learning curve, more YAML per route. I’ll take that over chasing controller-specific quirks.

Decision for me was straightforward: Gateway API is where traffic config is going; **Envoy Gateway** fits that story; migration effort looked bounded.

I did a **hard cutover** — no dual stack. Turn Traefik off, install Envoy Gateway, flip all routes in one go.

---

## What shipped

- **Routing:** Gateway API only — no Ingress objects. One Gateway with an HTTPS listener (443); everything maps through HTTPRoutes. Same hosts and paths as before, but structured resources instead of annotation graffiti.
- **TLS:** cert-manager — one consistent story for dev and prod (no “mkcert forever” in prod).
- **gRPC:** realm-core stays internal; no GRPCRoute for that yet. GRPCRoute is **ready** for future external gRPC (admin tools, mobile, whatever). Add routes when there’s a real consumer.
- **Tech-admin:** Lists Gateways, HTTPRoutes, GRPCRoutes instead of the old Ingress table. Same patterns — namespace selector, tables, YAML viewer — different resource types. I’m **not** exposing Envoy’s admin UI to the world; anything ops cares about goes through tech-admin.
- **Grafana:** Traefik dashboard is gone. I built a replacement for Envoy / Gateway API (routes, listeners, error rates). Nothing off-the-shelf fit; metrics exist, panels didn’t.

---

## What this buys me

Gateway API beats Ingress for the same reason everyone’s migrating: one model, fewer sharp edges, room to grow. If an external gRPC client shows up, **GRPCRoute** is there — no controller-specific duct tape refactor.

Envoy also lines up with how you’d do observability anyway: stats, tracing, access logs. If I later poke at a **service mesh**, the data plane story doesn’t fight this choice.

Yes, it’s **more** to learn and more YAML. No cute dashboard. For me the config is clearer and the direction is obvious.

---

## Rough edges and lessons

**Big-bang migration:** No parallel run, no nice rollback story — Traefik off, Envoy on, hope my checklist was complete. Fine for a **non-prod** lab setup; I’d stage it differently for a customer-facing cluster.

**Route matching order:** Gateway API has strict precedence (exact before prefix before method, etc.). Not the “custom order” games some Ingress controllers play. Know the rules or you’ll debug “why did that match?” at 2am.

**Dashboard tax:** Rolling my own Grafana board took real time. The Prometheus bits were there; making them readable wasn’t.

---

## Takeaway

Traefik did its job. **Ingress-as-primary** didn’t. Envoy Gateway + Gateway API is more work up front (especially tech-admin + Grafana), but traffic config is **one coherent layer** now — easier to extend and harder to regret.

**Current reference:** [Infrastructure — Edge traffic (Envoy Gateway)](../infrastructure.md#edge-traffic-envoy-gateway) summarizes what the cluster runs today (GatewayClass `eg`, single HTTPS listener, HTTPRoutes, cert-manager secret name, local 443 port-forward).
