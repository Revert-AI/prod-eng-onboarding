---
last_verified: 2026-08-07
owner: TBD (repo maintainer — update to whoever owns onboarding)
---

# Getting Started

Where to start if you're new to product construction at Revert AI. The onboarding path below is the main thing on this page — the accounts and tools sections exist so you can actually do it.

## Start here — the onboarding path

Five conversations, in this order. **The order is the point.** The thesis explains why the product exists, the consultants' work explains who it's for, and the architecture only makes sense once you have both. Going straight to the code is the most common way to end up with a working mental model of the systems and no idea what they're for.

1. **Revert's thesis** — what we're betting on, and why now.
   Ask **Rodrigo Terni**.
   Then read [Business & Strategy](../business-and-strategy/README.md).

2. **How consultants actually work** — the day-to-day this product exists to serve.
   Ask **Luis Leão**.
   Skim the [Glossary](../glossary/README.md) first if the vocabulary is new (*consultor* vs. *assessor*, fee-based vs. commission-based, AUM) — the conversation goes further when you're not decoding terms in real time.

3. **Product roadmap** — what's being built, in what order, and why that order.
   Ask **Matheus Fortes**.
   Then read [Projects](../projects/README.md).

4. **Nix** — the backend that owns consolidation, reconciliation, and the financial domain model.
   Ask **Daniel Vieira**.
   Then read [Product & Architecture](../architecture/README.md), and ask this repo's assistant to walk you through `nix_webserver` live.

5. **Bruxo** — the WhatsApp concierge agent advisors talk to.
   Ask **Guilherme Scagnolato**.
   Same [architecture overview](../architecture/README.md); ask the assistant about `concierge-agent-pi`.

Steps 1–3 are *why* and *for whom*. Steps 4–5 are *how*. If you only have time for two conversations this week, make them 1 and 2.

## Accounts & access

Sort these in parallel with the conversations above — you'll need them by step 4.

- **GitHub** — access to the `Revert-AI` organization. The repos you'll likely touch: `nix_webserver`, `portal_v2`, `concierge-agent-pi`, `revert-cloud-infra`, and `revert-knowledge-base` (see [Product & Architecture](../architecture/README.md)). Access is over SSH; confirm your key is on your GitHub account and authorized for the org.
- **Internal chat / communication tool** — `Not yet documented`. Ask your onboarding contact.
- **Email / SSO** — `Not yet documented`.
- **Linear** (project tracking, team `REV`) — see [Projects](../projects/README.md).

## Tools

- **git** and an SSH key registered with GitHub — required for everything in [Product & Architecture](../architecture/README.md).
- **An AI coding assistant** (e.g. Claude Code) — this repo is written for one. Clone it and the assistant reads [`AGENTS.md`](../AGENTS.md) to know how to answer your questions and when to consult the live repos or `revert-knowledge-base` directly.
- Repo-specific tooling (language runtimes, package managers, local dev setup) — `Not yet documented` here; each product repo should document its own setup.

## First tasks

1. Book the step 1 and step 2 conversations above — they're the ones that gate everything else.
2. Confirm you can reach the `Revert-AI` GitHub org and clone at least one product repo.
3. Ask your onboarding contact for the `Not yet documented` access items above.
4. Ask this repo's AI assistant something real — "how does the wallet flow work in `portal_v2`", "who owns the infra repo" — to confirm your access works end to end.
5. Read [Org & Teams](../org-and-teams/README.md) for who to ask about areas beyond the five above.
