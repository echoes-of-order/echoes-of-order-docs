# Devlog #2 – April 2026

## What this is about

From the outside it looks like “nothing changed”: same admin UI, same buttons. Under the hood, a chunk of how **Echoes of Order** talks to the **global game-data backend** is moving from **REST-shaped HTTP** to **gRPC** with a **single Protocol Buffer contract**.

That’s the kind of work nobody screenshots for a trailer — but it’s exactly the sort of plumbing that stops small changes from turning into five-file scavenger hunts.

---

## Why bother

For a long time, several places could end up defining or hand-rolling the “same” API: controllers here, fetch paths there, another client in a different service. When a field or a route moved, I was touching **multiple layers** to keep them in sync. Easy to miss one. Easy to ship a 404 or a silent mismatch.

**gRPC + protobuf** flip that story: the **contract lives in one place**. Services generate or load the same types. Adding a method or a field is a deliberate change to the schema — not a game of telephone across ad hoc JSON.

So the goal isn’t buzzword bingo. It’s **one language** between components, **fewer drift bugs**, and a path to extend admin and tooling without reinventing HTTP DTOs every time.

---

## What actually moved (in plain terms)

- **Admin-facing flows** that used to hit classic HTTP routes on the global backend increasingly go through an **admin database gRPC service**: one protobuf package, JSON wrapped where the UI still expects envelope-style responses.
- **Health and status** checks that used to piggyback on the same port as “real” admin calls got split onto **separate ports** where needed, so a lightweight process doesn’t accidentally answer **full** admin RPCs and return `UNIMPLEMENTED` — a boring detail until you’ve watched it happen in dev.
- **Examples of the payoff:** character list routes for the admin profile path, race base stats queries that broke when ORM property names didn’t match what TypeORM could filter on — those are the sorts of bugs that shrink when the **server** and **contract** are the source of truth, not scattered string paths.

I’m not claiming the migration is “done” everywhere. HTTP still exists where it should (browsers, public REST, legacy edges). This pass is about **tightening the internal spine** between tooling and global data.

---

## What you see vs what you don’t

**You don’t see** a new button or a renamed menu. **You might notice** fewer mysterious admin errors after a backend change — that’s the point.

**I see** fewer places to edit for one feature, and a clearer place to look when something breaks: proto + handler + bridge, instead of “which controller was this again?”

---

## How this fits the rest of the stack

This sits next to the **Envoy Gateway** story in [Devlog #1](2026-03-devlog-01-traefik-envoy-gateway-migration.md): edge routing is Gateway API; **in-cluster** and **tooling** traffic can stay typed on gRPC without turning every admin call into a public GRPCRoute. The high-level map is still [Architecture — communication](architecture.md#communication): HTTP/gRPC for request/response where it fits, Event Bus where the realm loop needs it.

---

## Rough edges

**Operational noise:** more moving parts (ports, which process owns which RPC set). Worth documenting and enforcing in config so local dev doesn’t “work by accident” on the wrong listener.

**Stub vs full service:** Any process that registers the **same** proto package but only implements **health** must not steal the port the **full** admin service uses. I learned that one the loud way.

**Human cost:** Migrating isn’t a weekend checkbox. It’s a lot of small, careful edits. The benefit shows up as **silence** — fewer regressions — which is a bad metric for fundraising screenshots but a good one for sleep.

---

## Takeaway

HTTP had its place; for **admin ↔ global data**, gRPC and a **central protobuf** are how I want to extend Echoes of Order without paying the “update five clients” tax every time.

If you’re supporting the project — see [For Sponsors](sponsor.md) — thank you. This layer doesn’t show up in a gameplay clip — it’s the kind of foundation that keeps the rest of the work honest.

**Related:** [Architecture](architecture.md) · [Infrastructure — component model](infrastructure.md#component-model) · [Devlog #1 — Envoy Gateway](2026-03-devlog-01-traefik-envoy-gateway-migration.md)
