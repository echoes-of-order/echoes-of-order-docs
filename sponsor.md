# For Sponsors

**Related docs:** [README](README.md) · [Current State](game-status.md) · [Project Goals](project.md) · [About the Developer](about-me.md)

*This page is the single source for support and community links — change it here only so links stay consistent.*

## What Is Echoes of Order?

Echoes of Order is a **systems-driven, persistent online world** (MMO-style). **Authority and simulation** sit at the center: one source of truth per realm, simulations that propose outcomes but never own state. The aim is a durable world where **infrastructure and correctness** lead — not a theme-park MMO or a disposable prototype.

## By the Numbers

Full metrics (LOC, services, explorations, diagrams): [Current State](game-status.md#by-the-numbers). See also [Explorations](explorations/README.md) and [Diagrams](diagrams.md).

## Why this project is run this way

Simulations propose; realm authority commits. That separation is the spine of the architecture (see [Architecture](architecture.md#authority--simulation)). I ship **explorations and decision records** so the reasoning stays visible over years. There is **no investor board** or commercial deadline stack. What you get as a reader is uneven velocity and blunt honesty about what is built and what is not.

Few public projects document the authority/simulation split with this much depth.

- **Authority-first:** The realm is the source of truth; nothing commits without validation.
- **Transparent:** Summaries live in this repo; full decision context sits in the main project under `docs/3_decisions`.
- **Independent:** Solo, spare-time work — correctness and structure beat feature hype.

## What Exists Today

A working multi-service backend (Kubernetes, realm isolation, domain engines) is in place. There is **no publicly playable game yet**. Detail: [Current State](game-status.md#what-exists).

## What Your Support Enables

Funding keeps the work **independent**: time for open explorations, published trade-offs, and docs that stay accurate as the monorepo moves — without cutting corners for someone else's roadmap.

Ways to contribute:

- **[Patreon](https://www.patreon.com/c/EchoesOfOrder)** · **[GitHub Sponsors](https://github.com/sponsors/echoes-of-order)** · **[Ko-fi](https://ko-fi.com/echoesoforder)**
- **[GoodCrowd.org](https://www.goodcrowd.org/echoes-of-order-mein-mmo-traum-braucht-dich)** — social crowdfunding (non-profit platform; [goodcrowd.org](https://goodcrowd.org/) overview)
- **[GoFundMe](https://gofund.me/4b9184a6a)** — same campaign on GoFundMe for donors who prefer that flow
- **[Liberapay](https://liberapay.com/)** for recurring support in many regions (a dedicated project page may follow)

*Note:* Fees, payout rules, and availability differ by platform and country. This page remains the neutral list of official links.

## Who Is Behind It

**André Jens Meyer** — senior full stack engineer and DevOps focus, 15+ years, Germany. Check24 (7+ years), own companies, Leipzig Coding Contest 2011. Solo build; spare time. Full CV and stance: [About the Developer](about-me.md).

## How to Follow Updates

- **Docs:** [Current Work](current-work.md), [Explorations](explorations/README.md), and [Devlogs](devlogs/README.md) when something material ships.
- **Social:** [X (Twitter)](https://x.com/EoO_MMORPG), [itch.io](https://echoes-of-order.itch.io/). If X is not reachable where you are, the docs above are the main channel.

No release calendar — only continued focus on correctness, clarity, and transparency.
