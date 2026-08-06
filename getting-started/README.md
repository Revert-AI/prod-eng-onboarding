---
last_verified: 2026-08-06
owner: TBD (repo maintainer — update to whoever owns onboarding)
---

# Getting Started

A first-day checklist for anyone joining product construction at Revert AI. The exact account/tool list below is a starting structure — a few items are marked `Not yet documented` where this session had no way to verify company-specific logistics (HR systems, physical/remote policy, internal chat). Whoever owns onboarding should fill those in and update `last_verified` above.

## Accounts & access

- **GitHub** — you'll need access to the `Revert-AI` GitHub organization. The core repos you'll likely touch: `nix_webserver`, `portal_v2`, `concierge-agent-pi`, `revert-cloud-infra`, and `revert-knowledge-base` (see [Product & Architecture](../architecture/README.md)). Access is via SSH; confirm your key is added to your GitHub account and to the org.
- **Internal chat / communication tool** — `Not yet documented`. Ask your onboarding contact which tool the team uses day-to-day.
- **Email / SSO** — `Not yet documented`.
- **Linear** (project tracking, team `REV`) — see [Projects](../projects/README.md).

## Tools

- **git** and an SSH key registered with GitHub — required for everything in [Product & Architecture](../architecture/README.md).
- **An AI coding assistant** (e.g. Claude Code) — this repo is written for one. Clone it, and the assistant reads [`AGENTS.md`](../AGENTS.md) to know how to answer your questions and when to consult the live repos or `revert-knowledge-base` directly.
- Repo-specific tooling (language runtimes, package managers, local dev setup) — `Not yet documented` here; each of the four product repos should document its own setup in its own README once F4's deeper research pass covers them.

## First tasks

1. Confirm you can reach the `Revert-AI` GitHub org and clone at least one of the four product repos.
2. Ask your onboarding contact for `Not yet documented` access items above.
3. Ask this repo's AI assistant a question about the product, the org, or the business — e.g. "how does the wallet flow work in portal_v2" or "who owns the infra repo" — to confirm your access actually works end to end.
4. Read [Org & Teams](../org-and-teams/README.md) to find out who to ask about a given area.
