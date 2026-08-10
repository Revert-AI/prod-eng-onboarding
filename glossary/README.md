---
last_verified: 2026-08-07
owner: TBD (repo maintainer — update to whoever owns this content)
---

# Glossary

The vocabulary you need to follow a conversation, a Linear ticket, or a pull request at Revert. Definitions are grounded in what `revert-knowledge-base` and the product code actually say — where a term is used without ever being defined, this page says so rather than guessing.

**Scope of the research behind this page.** It was built from the paths this repo is allowed to read (`company/about revert/`, `market/`, `gtm/`, `product/`) plus the product repos. `sales/`, `regulation/`, `company/fundraising/` and `company/atas/` were never read. So **"undefined" and "unresolved" here mean "not found in those paths"** — not "does not exist". Several of the open acronyms below may well be defined somewhere this page couldn't look.

Marked `[inferred]` = extended beyond what the source states. Marked 🚩 = **the obvious reading misleads** — whether because the everyday meaning is wrong, because the term is Revert-specific, or because it's outdated and you need to check the date.

This is a static snapshot for **vocabulary**. It carries a few illustrative figures, but treat any number here as needing re-verification against `revert-knowledge-base` live (per [`AGENTS.md`](../AGENTS.md)) before you rely on it — current pricing, market data and strategy live there, not here.

## Read this first — terms that mislead

These are the ones that cost people a day. Every row is a word whose everyday meaning is wrong here.

| Term | You'd assume | It actually means |
|---|---|---|
| **Wallet** (carteira) | The client's whole portfolio | **One custody account at one broker.** A client has several. The consolidated view is an **Aggregation**. |
| **Comply** / `conciliation_policy` | Regulatory compliance | Which side wins a reconciliation dispute: `COMPLY_BROKER` (broker is truth) or `COMPLY_TRADER` (our number is truth). Nothing to do with compliance. |
| **Persona** | A UX archetype | A real person or company in a database table — client, prospect, or banker. Covers both individuals and legal entities. |
| **Aggregation** | A database `GROUP BY` | A logical filter defining which wallets/assets belong in a view or report. |
| **Nix** | Just the backend | Both the consultant-facing operational product **and** one side of every reconciliation ("NIX vs. broker"). "The NIX value is wrong" means our internal number, not that the system is down. |
| **Tenant** | Our consultant client | In code, usually the **legacy schema-per-firm layer**. The canonical product model is different — see the entry below. |
| **Booking** | Scheduling something | Registering a movement in ComDinheiro after reconciliation. |
| **B2B / B2C** in a doc | Revert's own segments | **Market terminology** — B2B is the brokerage-serving-advisory-firms channel. Revert runs one active business model, Full Service; it does not describe itself in B2B/B2C terms. |
| **MovementInserter** | A service class | A **model** (the canonical entry record), despite the name. |

## Revert's business model

- **Full Service** — the only active business model. An investment professional (assessor, consultor, banker) operates **under Revert's CVM consultancy**: Revert signs underneath and provides the CVM licence, compliance, consolidation, reporting, agents, billing and PJ2. Tripartite contract (consultant + Revert + end client). *Sole active model since 26/05/2026.*
- **Tech Service** 🚩 — an existing family office or advisory firm contracting Revert as operational infrastructure inside their own structure. **Shelved since 26/05/2026** — historical reference only, not current revenue and not a roadmap driver. Much of the knowledge base and legacy code was written during this era, so **check the date on any older document**.
- **Autopilot vs. Copilot** — the positioning line. Competitors ship a *tool* (copilot); Revert delivers *the finished work* (autopilot). Practical product consequence, quoted internally: *"Dashboard is a consequence; the work getting done is the product."*
- **Maia vs. Bruxo** 🚩 — two conversational surfaces with a hard boundary. **Maia** serves the **end client** (personal-banker style, WhatsApp/email). **Bruxo** serves the **consultant** and is their bridge into Nix. The stated rule: *"Bruxo is not the client's agent. Bruxo is the Consultant's agent."*
- **Ekho** (also written Eko / ECHO) — the family office Revert spun out of; today the real operating environment, and a separate legacy schema in the database. **Don't generalize Ekho-specific behavior into product requirements** — the knowledge base says this explicitly.
- **PJ2** — revenue lines beyond the advisory fee: insurance, consórcio, home equity, FX, credit. The acronym is never expanded anywhere. `[inferred]` likely "second legal entity / second product line."
- **Marreta / marretar** 🚩 — internal slang for **forcing a number into the database** (a price or quantity accommodation) instead of genuinely reconciling it. Root cause of the corrupted-history onboarding problem; surfaces in code as `marretator_calculator` and `is_artificial`. The docs use the word without defining it.
- **The four waves** — the market narrative used in positioning: closed bank (1990s) → open brokerage (2000s) → scaled advisory (2010s) → **independent consultancy (2020s)**. An earlier three-wave version exists in the same file and is explicitly superseded by this one.

## The Brazilian wealth market

Figures below are approximate and mostly undated in the source — treat them as orders of magnitude, not current metrics.

- **Assessor / AAI** (Agente Autônomo de Investimentos) — tied to an intermediary (XP, BTG), paid by **commission** on product distribution, exclusivity required at BTG. ~27.6k licensed (ANCORD, Feb 2026).
- **Consultor CVM** — registered under RCVM 19, paid a **fee by the client**, no exclusivity, multi-custody. A far smaller base but growing several times faster.
- **Banker** — private banker at a large bank. Different fear from the assessor's: *"will the client come with me?"* (brand over person) rather than *"can I operate on my own?"* (infrastructure).
- **Fee-based vs. commission-based** — the structural transition underpinning Revert's thesis. Brazil is still overwhelmingly commission-driven; the US is majority fee-based; Europe banned commission. The knowledge base frames it as **two transitions at once**: pay model *and* role — from tied distribution to independent advice.
- **Custodiante / broker** 🚩 — where the client's money actually sits. **In Nix code, "broker" means brokerage and custodian interchangeably.** Access quality varies sharply: real APIs only for XP and BTG; semi-automatic for Itaú and Avenue; file-based (PDF/CSV/XML) for the rest, with formats that change every few months.
- **Homologação** — an institution authorizing a given consultant to reach its APIs and automated flows. Recorded insight: *"the barrier to entry isn't just internal technology or CVM registration. It's institutional access."* A small consultant can't get homologated alone — one of the central justifications for Full Service.
- **Family office / MFO** — operationally distinct from a consultant in one way that matters: **a family office reconciles** (and carries a long onboarding); a consultant/assessor generally doesn't, accepts what the broker reports, and onboards with near-zero operational weight.
- **AUM vs. AuC vs. AUB vs. AUS** 🚩 — four similar-looking acronyms for four different slices of "how much money." **AUM** (Assets Under Management) and **AuC** (Assets under Custody) are standard market terms. **AUB** (Asset Under Billing) is flagged in the knowledge base as *canonical Revert vocabulary* — the **billable slice** of a client's assets, which is not necessarily total AUM (a client can hold assets Revert doesn't bill on). **AUS** is a fourth value living in code, not market usage — see [Acronyms nobody has expanded](#acronyms-nobody-has-expanded) below; nothing in the sources this page could read states what distinguishes it from AUM, so don't assume it's just a variant spelling.
- **bps / ROA** — basis points (1 bp = 0.01%), the standard unit for pricing and margin. ROA = revenue ÷ AUM.
- **Captação líquida (NNM)** — net new money. The hard part is separating genuinely new money from reinvested yield; Revert's current approach is inference-based, *"small error, but not deterministic across all sources."*

## Regulatory

- **RCVM 19** (in force Apr 2021) — securities consultancy; separated advice (fee) from distribution (commission).
- **CVM 178 / 179** (in force 2024) — advisory plus transparency. **179** requires a quarterly statement itemizing what the client paid in commission. Recorded observation: it did *not* move end clients much; the real effect was on **supply** — it gave professionals a formal argument to migrate.
- **CVM 175** (in force Oct 2023) — the new fund framework.
- **Lei 14.754/23** — closed-end fund taxation; triggered migration from closed funds toward managed portfolios.
- **PJ** — the contracting model Revert uses. Specifics (entity structure, what it means for your own contract) are a People/Legal question, not a glossary one.
- **Suitability / KYC** — being built as first-class onboarding/compliance surfaces, and a pillar of the trust moat: *"A financial agent without auditability is a toy."* In research, `suitability` acts as a **gate above status** — an "Approved" fund can still be blocked by it.

## Pricing

- **Repasse regressivo** — the Full Service revenue-share model, in which the share retained by the consultant **decreases over the first years** of the contract. **PJ2 carries its own separate pass-through rate.** Current percentages, the pass-through rate and billing mechanics live in `revert-knowledge-base`, deliberately not here — they change, and this page is not the place people should be quoting a rate from.
- **Advisory fee / management fee / performance fee / minimum fee** — the four components Nix's billing has to model, per wallet, with a calculation trail. Brazilian day-count default is **BD_252**. **Known gap, documented:** there is *no explicit high watermark* — performance fee is computed period by period with no memory of prior peaks.

## Product & data model

Where business language meets what the database actually stores.

- **Wallet** 🚩 — one custody account at one broker (unique on `(wallet_nix, broker)`). Carries the reconciliation policy and lock dates.
- **Aggregation** 🚩 — the consolidated view. *"Not a real financial entity — a logical filter defining which wallets/assets to include."* Built from wallet-split and asset-exclusion rules; its `is_fully_conciliated` property gates reporting.
- **Persona** 🚩 — the central registry entity, covering individuals and companies, and simultaneously client, prospect and banker. Known as the "persona god-table" internally, with a stated direction to break it apart.
- **Tenant** 🚩 — **two layers coexist, and this is the most consequential ambiguity in the backend.** The canonical product model is *"the advisor is the real tenant"*, with isolation enforced by **Postgres row-level security** keyed off the advisor — explicitly *"not merely a Django/DRF filter convention."* The legacy layer is `django-tenants`, **one schema per firm**, which today mostly separates the Revert schema from the Ekho one. In `settings.py` and decorators, "tenant" almost always means the legacy firm layer. Some older architecture docs describe RLS as a DRF filter and carry a correction note saying that reading is incomplete.
- **Position vs. Movement** — a **Position** is a daily snapshot per `(date, asset, wallet)` carrying quantity, values, **PU** (unit price) and a battery of PnL/return windows. A **Movement** is an event (a trade). Movements flow `MovementInserter` → `MovementBooking` → `BrokerMovement`.
- **Conciliação** 🚩 — comparing the Nix side against the broker side, by type (`MOVEMENT` or `POSITION`). **It is not a line-by-line match**: the engine aggregates by key (`broker + wallet + asset + movement_type` per day) and compares totals — a documented risk, since it *"can mask offsetting trades."* Tolerance margin is configurable per broker/asset.
- **Override / EOD** — manual or batch resolution of a divergence; EOD is the daily close that triggers per-wallet booking.
- **ComDinheiro (CMD)** — the Brazilian platform serving as both market-data source and external calculation/quotização engine. Stated architectural posture: *"Valuation is replaceable"* — keep the dependency isolated enough to swap.
- **Brazilian mechanics modeled directly** — **come-cotas** (`CC`, automatic fund taxation on the last business day of May and November), **JCP**, **aporte/resgate**, **split vs. inplit**, and the invented verb `quotizate_wallets`. A corporate action *becomes* a `MovementInserter` to enter the booking pipeline.
- **`country_scope`** (ONSHORE / OFFSHORE) — with an explicit warning: the classification is **relative to viewer and broker context**, not an intrinsic property of a position.

## Investments & research

Second-week vocabulary — needed if you touch portfolios or research.

- **Vetor de risco** 🚩 — **a Revert-specific concept.** Assets are classified by what has to happen for them to make or lose money, and what they suffer alongside — *instead of* by commercial product category. Seven vectors, from defensive/post-fixed through alpha, credit, listed real-estate credit, real-estate income, market beta, and beta-credit hybrid. Boundary rule: *"classify by behavior under stress, not by the commercial fact sheet."*
- **FII de papel vs. FII de tijolo** 🚩 — paper FIIs hold real-estate **credit** (CRI) and belong in the credit block; brick FIIs own rented **property** and belong in real-estate income. Same legal form, same tax exemption, *"but they lose money through different engines."* Calling "FII" a single class when both are mixed is explicitly prohibited in client language.
- **Debênture incentivada** 🚩 — coined internally as a **beta-credit hybrid**: despite being fixed income, it can lose heavily with no default at all, via duration, spread and redemption flow. Rule: *"must not be called defensive merely because it is fixed income."*
- **Research status vocabulary** — `Aprovado`, `Portfolio`, `Hold`, `Vetado`, and the critical rule that **research status does not substitute for portfolio policy** (an approved fund can still be excluded on sizing or overlap). A **veto qualitativo** disqualifies a manager regardless of the diversification math. A **lacuna** (evidence gap) must be recorded explicitly — *"a gap is part of the output"* — never filled with outside opinion.
- **Janela de cotação** — the secondary-market quotation window, Mon–Fri **10:00–15:00**. One of the most directly codifiable rules in the investments material.

## Where the sources contradict each other

Genuinely unresolved within the paths this page could read. If you hit one, ask — don't pick a side silently.

- **Guardian / Guardião** — described in one place as a deterministic, LLM-free controller for agent-container lifecycle, and in another as a security layer filtering prompt injection. **These are not compatible.**
- **Bushido** — described as a reconciliation agent doing heavy mathematical validation in one document, and as an operational Nix executor / middle-office in more recent ones. `[inferred]` the role evolved, but nothing states it.
- **"Nyx" vs. "Nix"** — one document writes the API as "Nyx"; everything else writes "Nix". `[inferred]` a typo — worth confirming.
- **COI** — in an archived GTM context it means *Center of Influence*, a partnership channel. In a market context it appears where the text almost certainly means **COE** (*Certificado de Operações Estruturadas*); `[inferred]` a transcription slip.

## Acronyms nobody has expanded

Used across the knowledge base and code with the meaning taken for granted and the expansion never written down. Listed so you know these are genuinely open in the paths this page could read — worth asking about, and worth capturing here once answered.

`NIX` (meaning known, expansion not) · `PJ2` (meaning known, expansion not) · `RPE` — the highest-value unknown, appearing in movement-sync services, forced-value statuses and an override endpoint · `AUS` — the default `aggregation_type`, while a sibling config defaults to `AUM`, with no stated difference (see the AUM/AuC/AUB/AUS entry above) · `IPS` (`[inferred]` Investment Policy Statement) · `gross_up_value`

Standard market acronyms are treated as primitives and also never expanded: `CDI`, `IPCA`, `FGC`, `PDD`, `PL`, `B3`, `ANBIMA`.
