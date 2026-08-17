# prod-eng-onboarding

The onboarding entrypoint for anyone building the product at Revert AI — engineers, and anyone
else working on product construction.

## How this repo is meant to be used

1. **Clone it.**
2. **Ask an AI assistant** (Claude Code or similar) questions about the product, the org, the
   architecture, the business model, or ongoing projects.

The assistant reads [`AGENTS.md`](AGENTS.md) to know what's answered from this repo directly and
what it needs to fetch live — from the four product repos, `revert-knowledge-base`, Linear, or
Notion. You generally don't need to open `AGENTS.md` yourself; it's written for the assistant, not
for you. Open it only if you're curious how the routing works or you're extending it.

## New here? Start with Getting Started

Don't jump straight to the architecture section below — [`getting-started/README.md`](getting-started/README.md)
walks through a short, ordered sequence of conversations (with named people to ask) before the
docs make full sense on their own. If you ask the assistant "where do I start," it will point you
there too.

## Repo map

| Section | What's there |
|---|---|
| [Getting Started](getting-started/README.md) | The onboarding sequence, accounts/access, tools, first tasks |
| [Glossary](glossary/README.md) | Revert-specific vocabulary — including terms whose everyday meaning is wrong here |
| [Org & Teams](org-and-teams/README.md) | Who to ask about what, and who commits where |
| [Business & Strategy](business-and-strategy/README.md) | Strategy framing; points live to `revert-knowledge-base` for anything time-sensitive |
| [Product & Architecture](architecture/README.md) | What the product does and how the systems fit together; points live to the four product repos |
| [How We Work](how-we-work/README.md) | How work is born, decided, specified and shipped; points live to the process doc in Notion |
| [Projects](projects/README.md) | Pointer to Linear for current work |

Most of these sections are a **thin static overview plus a live pointer**, not the full source of
truth — that's deliberate. Static content carries a `last_verified` date in its frontmatter; treat
anything older than ~90 days as due for a refresh.

## Access

This repo is internal, written for people building the product. It carries business-model detail
and candidly records known product weaknesses — that's useful, but it means the content is written
for restricted circulation, not general distribution. See `AGENTS.md`'s "Access assumption" note
before pulling content out of this repo into somewhere more widely read.

## Contributing

This repo evolves PR-driven, by norm rather than by strict process. If you're adding or refreshing
content sourced from `revert-knowledge-base` or the four product repos, open a PR rather than
committing directly — see `AGENTS.md`'s "Content drafting sessions" section for the mechanics
(sparse-checkout scoping, secret-screening, what stays out of this repo).
