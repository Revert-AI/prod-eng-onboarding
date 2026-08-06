---
last_verified: 2026-08-06
owner: TBD (repo maintainer — update to whoever owns this content)
---

# Business, Strategy & Financial Glossary

This section is a **thin static overview**, not the source of truth. It exists so a reader gets useful
orientation immediately; anything deeper or time-sensitive should be pulled live from
`revert-knowledge-base` per the instructions below, not from this file.

## Financial glossary

A few terms that recur across Revert's business and market discussions:

- **AUM (Assets Under Management)** — the total client assets a firm (or Revert's advisor network) manages;
  the standard unit used to size the wealth-management market and individual books of business.
- **Fee-based vs. commission-based** — the two dominant advisory revenue models. Commission-based pays the
  advisor per product sold; fee-based charges a transparent percentage of AUM. Brazil's market is described
  as still commission-heavy today, transitioning toward fee-based — a trend already further along in the US
  and largely completed in Europe.
- **ROA (Return on Assets)** — a fee-rate benchmark expressed as a percentage of AUM; used in market
  discussions as shorthand for how much revenue a firm or advisor generates per unit of assets managed.
- **Full Service vs. Tech Service** — Revert's own two business-model tracks. Full Service means Revert
  operates the entire consultancy for an independent advisor (compliance, tech, billing, the works). Tech
  Service meant selling backend technology to existing wealth firms. As of the most recent internal update,
  Full Service is the only active model; Tech Service is kept as historical reference only.
- **PJ2** — Revert's term for cross-sell revenue lines layered on top of the core advisory fee (e.g.
  insurance, credit, consortium, FX), rather than a data field. It's product terminology internal to Revert.
- **Consultor vs. Assessor** — the two investment-advisor archetypes central to the market thesis: a
  *consultor* is a CVM-registered independent investment consultant paid directly by the client; an
  *assessor* is affiliated with and paid indirectly through a brokerage.

## Strategy framing

Revert builds AI-agent infrastructure aimed at chronic operational problems in Brazilian wealth
management — consolidating data from disparate custodians, reconciling positions, generating performance
reports, and calculating billing. Its positioning draws a deliberate line between "autopilot" (delivering
the finished operational service) and "copilot" (handing someone a tool and leaving them to run it) —
Revert positions itself as the former. That bet is set against a market-wide shift already underway in
Brazil: advisors and consultants moving away from commission-based, brokerage-affiliated models toward
independent, fee-based practice, a transition the market data describes as further along in the US and
essentially complete in Europe.

This overview intentionally stops here. Revert's live strategy, moat thinking, market data, and go-to-market
material change often and are owned by `revert-knowledge-base` — see below for how to reach it.

## For deeper or current detail: consult `revert-knowledge-base` live

Do not treat this file as up to date on anything beyond the glossary terms above. For real business-model
detail, current market data, or go-to-market status, live-consult `revert-knowledge-base`'s
`company/about revert/`, `market/`, and `gtm/` folders — follow the root `AGENTS.md`'s
`revert-knowledge-base` instructions exactly (clone command, `--no-cone` sparse-checkout, the required
`git checkout` step, and the excluded-path list), rather than the steps being repeated here. This file
intentionally does not restate that mechanism — a second copy would drift from `AGENTS.md` the first time
either one is edited alone.
