---
last_verified: 2026-08-07
owner: TBD (repo maintainer — update to whoever owns this content)
---

# Product & Architecture

## What the product does

Revert is the system of record and daily working surface for an independent Brazilian wealth
advisor's book of client portfolios. High-net-worth clients hold assets across multiple brokers
and custodians (e.g. XP, BTG, Itaú, offshore accounts, funds, fixed income, alternatives); no
single broker sees the whole picture. Revert pulls holdings from wherever they sit, reconciles and
prices them into one consolidated view, and turns that into investor reports, allocation analysis,
billing, and conversational-agent workflows.

The primary customer is the independent advisor (the *consultor*) — Revert is operational
infrastructure for advisors, not a retail or robo-advisor app for end consumers. Three systems make
up the current architecture: a Django/DRF backend that owns consolidation, reconciliation, and the
financial domain model; a React/TypeScript web portal advisors and operators use day to day; and an
LLM-based concierge agent that lets advisors work the same core over WhatsApp. Cloud infrastructure
(AWS via Terragrunt/OpenTofu) underpins all of it. Multi-tenancy is advisor-first, with
database-enforced isolation as the correctness boundary.

This is a thin, static overview only. Anything about a specific repo's current code, deploy state,
or design detail should be answered by consulting that source live, not by trusting this file —
see the pointer table below.

## Deep dive: `nix_webserver`

Nix is the monolith — the system with the most surface area and the highest blast radius, and the
one most worth understanding in depth before touching it. Two static reference documents go well
beyond this page's overview:

- [`nix-webserver/architecture.html`](nix-webserver/architecture.html) — runtime topology (the one
  image, five ECS Fargate services), the request path through the middleware stack, multi-tenancy
  and Row-Level Security (the two coexisting isolation layers — see the [Glossary](../glossary/README.md)'s
  `Tenant` entry for the vocabulary), and the money path from ingestion through reconciliation,
  booking, and billing.
- [`nix-webserver/data-model.html`](nix-webserver/data-model.html) — what every table inherits
  (history mirroring, soft delete, decimal-for-money), the core Persona/Wallet/Asset/Position
  entities and how RLS turns their foreign-key topology into an access policy, and the asset
  catalog's exclusive-subtype pattern.

Both are **static HTML, in Portuguese**, captured `2026-08-07` directly from the `nix_webserver`
repo (code, task definitions, Terragrunt, and its own `_bmad-output/` doc set) — open them in a
browser, not as markdown. Treat them the same way as the rest of this section: a point-in-time
snapshot, not a live source. Re-verify against the repo (or regenerate) once they're a few months
stale, and re-run the secret-screening check below on any refresh, since they were built from a
live consultation of the repo.

## Sources — consult live for anything time-sensitive

The table below names each source and its one-line purpose. Per the tool-precedence and
secrets-screening conventions in the root `AGENTS.md`: prefer `gh`/git over SSH for every
GitHub-hosted source below (WebFetch is not a functional fallback for these private repos without
separately configured authentication); for `revert-knowledge-base`, use sparse-checkout scoped to
`product/` only, cloned outside this repo's working tree, per `AGENTS.md`'s instructions; and before
quoting or summarizing anything fetched live from the 4 architecture repos, screen it for
secret/credential shapes (API keys, private keys, `.env`-style assignments, connection strings) and
decline to surface a match, flagging it as a security concern instead — `revert-cloud-infra` is
infrastructure and warrants the closest look.

| Source | Type | One-line purpose |
|---|---|---|
| `nix_webserver` | GitHub repo (Revert-AI) | The backend: Django/DRF + PostgreSQL service ("Nix") owning consolidation, reconciliation, the financial domain model (assets, positions, movements), billing, and multi-tenant/RLS isolation. |
| `portal_v2` | GitHub repo (Revert-AI) | The frontend web portal: React + TypeScript + Vite app advisors and operators use for day-to-day work; deploys to multiple environments (homolog, tests, demo, prod). |
| `concierge-agent-pi` | GitHub repo (Revert-AI) | "Bruxo," the advisor-facing concierge agent: an LLM working over the Nix backend and a small toolset, reached by advisors over WhatsApp; in production today, rebuilding the agent on an embedded "Pi" engine. |
| `revert-cloud-infra` | GitHub repo (Revert-AI) | AWS infrastructure as code (Terragrunt + OpenTofu): VPC, ECS Fargate, ALB, ECR, and the application services that run on them. |
| `revert-knowledge-base` (`product/` folder only) | GitHub repo (Revert-AI), sparse-checkout | Deeper, maintained technical documentation per repo — per-Django-app breakdowns, deploy/infra/integration references, and related product docs — beyond what this overview covers. Not yet documented here in more depth; consult it directly. |

Not yet documented in this overview: per-service deployment runbooks, the full list of external
integrations (brokers, market data, communications), and the internal agent-control-plane
("Guardian") that manages agent containers — all live in the sources above, not here.
