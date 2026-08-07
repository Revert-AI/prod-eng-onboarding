---
last_verified: 2026-08-07
owner: TBD (repo maintainer — update to whoever owns this content)
---

# Glossary

The vocabulary you need to follow a conversation, a Linear ticket, or a pull request at Revert. Definitions here are grounded in what `revert-knowledge-base` actually says — where the knowledge base uses a term without defining it, this page says so rather than guessing.

Marked `[inferred]` = extended beyond what the knowledge base states. Marked 🚩 = **a term that commonly gets misread**; the "Terms that mislead" table below collects the worst offenders.

This is a static snapshot. For current business detail — strategy, market data, pricing in force — consult `revert-knowledge-base` live per [`AGENTS.md`](../AGENTS.md); this page is for vocabulary, not for current numbers.

## Read this first — terms that mislead

These are the ones that cost people a day. Every row is a word whose everyday meaning is wrong here.

| Term | You'd assume | It actually means |
|---|---|---|
| **Wallet** (carteira) | The client's whole portfolio | **One custody account at one broker.** A client has several. The consolidated view is an **Aggregation**. |
| **Comply** / `conciliation_policy` | Regulatory compliance | Which side wins a reconciliation dispute: `COMPLY_BROKER` (broker is truth) or `COMPLY_TRADER` (our number is truth). Nothing to do with compliance. |
| **Persona** | A UX archetype | A real person or company in a database table — client, prospect, or banker. Covers both individuals and legal entities. |
| **Aggregation** | A database `GROUP BY` | A logical filter defining which wallets/assets belong in a view or report. Hierarchical, rule-driven. |
| **Nix** | Just the backend | Both the consultant-facing operational product **and** one side of every reconciliation ("NIX vs. broker"). "The NIX value is wrong" means our internal number, not that the system is down. |
| **Tenant** | Our consultant client | In code, usually the **legacy schema-per-firm layer** (`django-tenants`), which today mostly separates Revert from Ekho. The canonical product model is "the advisor is the tenant", enforced via Postgres RLS. Two layers coexist. |
| **Booking** | Scheduling something | Registering a movement in ComDinheiro after reconciliation. |
| **B2B / B2C** in a doc | Revert's segments | **Market terminology**, not Revert segments — B2B means the brokerage-serving-advisory-firms channel. Revert has had one segment since 26/05/2026: Full Service. |
| **MovementInserter** | A service class | A **model** (the canonical entry record), despite the name. |

## Revert's business model

- **Full Service** — the only active business model. An investment professional (assessor, consultor, banker) operates **under Revert's CVM consultancy**: Revert signs underneath and provides the CVM licence, compliance, consolidation, reporting, agents, billing and PJ2. Tripartite contract (consultant + Revert + end client). *Sole active model since 26/05/2026.*
- **Tech Service** 🚩 — an existing family office or advisory firm contracting Revert as operational infrastructure inside their own structure. **Shelved since 26/05/2026** — historical reference only, not current revenue and not a roadmap driver. Much of the knowledge base and legacy code was written during this era, so **check the date on any older document**.
- **Autopilot vs. Copilot** — the positioning line. Competitors ship a *tool* (copilot); Revert delivers *the finished work* (autopilot). Practical product consequence, quoted internally: *"Dashboard is a consequence; the work getting done is the product."*
- **Maia vs. Bruxo** 🚩 — two conversational surfaces with a hard boundary. **Maia** serves the **end client** (personal-banker style, WhatsApp/email). **Bruxo** serves the **consultant** and is their bridge into Nix. The stated rule: *"Bruxo is not the client's agent. Bruxo is the Consultant's agent."*
- **Ekho** (also written Eko / ECHO) — the family office Revert spun out of; today the anchor client and real operating environment, and a separate legacy schema in the database. **Don't generalize Ekho-specific behavior into product requirements** — the knowledge base says this explicitly.
- **PJ2** — revenue lines beyond the advisory fee: insurance, consórcio, home equity, FX, credit. The knowledge base never expands the acronym. `[inferred]` likely "second legal entity / second product line."
- **Marreta / marretar** 🚩 — internal slang for **forcing a number into the database** (a price or quantity accommodation) instead of genuinely reconciling it. Root cause of the corrupted-history onboarding problem; surfaces in code as `marretator_calculator` and `is_artificial`. The docs use the word without defining it.

## The Brazilian wealth market

- **Assessor / AAI** (Agente Autônomo de Investimentos) — tied to an intermediary (XP, BTG), paid by **commission** on product distribution, exclusivity required at BTG. ~27.6k licensed (ANCORD, Feb 2026).
- **Consultor CVM** — registered under RCVM 19, paid a **fee by the client**, no exclusivity, multi-custody. A far smaller base (~2.3k active) but growing several times faster.
- **Banker** — private banker at a large bank. Different fear from the assessor's: *"will the client come with me?"* (brand over person) rather than *"can I operate on my own?"* (infrastructure).
- **Fee-based vs. commission-based** — the structural transition underpinning Revert's thesis. Brazil is still ~90% commission revenue; the US is ~72–75% fee-based; Europe banned commission. The knowledge base frames it as **two transitions at once**: pay model *and* role — from tied distribution to independent advice.
- **Custodiante / broker** 🚩 — where the client's money actually sits. **In Nix code, "broker" means brokerage and custodian interchangeably.** Access quality varies sharply: real APIs only for XP and BTG; semi-automatic for Itaú and Avenue; PDF/CSV/XML for the rest. *"Itaú sends PDFs, Bradesco CSVs, Safra XMLs. The formats change every 6 months."*
- **Homologação** — an institution authorizing a given consultant to reach its APIs and automated flows. Recorded insight: *"the barrier to entry isn't just internal technology or CVM registration. It's institutional access."* A small consultant can't get homologated alone — one of the central justifications for Full Service.
- **Family office / MFO** — operationally distinct from a consultant in one way that matters: **a family office reconciles** (and carries a ~30-day onboarding); a consultant/assessor generally doesn't, accepts what the broker reports, and onboards with near-zero operational weight.
- **AUM / AuC / AUB** — Assets Under Management; Assets under Custody; and **AUB (Asset Under Billing)**, flagged in the knowledge base as *canonical Revert vocabulary* — the **billable slice** of a client's assets, which is not necessarily total AUM.
- **bps / ROA** — basis points (1 bp = 0.01%), the standard unit for pricing and margin. ROA = revenue ÷ AUM. A recurring sales anchor: the cost of running operations manually lands somewhere in the **9–34 bps** range, *"scattered across salaries and invisible to the decision-maker."*
- **Captação líquida (NNM)** — net new money. The hard part is separating genuinely new money from reinvested yield; Revert's current approach is inference-based, *"small error, but not deterministic across all sources."*

## Regulatory

- **RCVM 19** (in force Apr 2021) — securities consultancy; separated advice (fee) from distribution (commission).
- **CVM 178 / 179** (in force 2024) — advisory plus transparency. **179** requires a quarterly statement itemizing what the client paid in commission. Recorded observation: it did *not* move end clients much; the real effect was on **supply** — it gave professionals a formal argument to migrate.
- **CVM 175** (in force Oct 2023) — the new fund framework.
- **Lei 14.754/23** — closed-end fund taxation; triggered migration from closed funds toward managed portfolios.
- **PJ structure** — Revert is incorporated in Delaware, **cannot hire CLT**, and works exclusively with PJ. Its CVM consultancy CNPJ has been open since April 2026.
- **Suitability / KYC** — being built as first-class onboarding/compliance surfaces, and a pillar of the trust moat: *"A financial agent without auditability is a toy."* In research, `suitability` acts as a **gate above status** — an "Approved" fund can still be blocked by it.

## Pricing

- **Repasse regressivo 90/80/70** — the Full Service reference: the consultant keeps **90%** of revenue in year 1, **80%** in year 2, **70%** from year 3 on. No signup fee, no upfront investment. PJ2 pays through at **50%**. Billing runs via direct account debit through the XP/BTG partnership — no boleto.
- **Advisory fee / management fee / performance fee / minimum fee** — the four components Nix's billing has to model, per wallet, with a calculation trail. Brazilian day-count default is **BD_252**. **Known gap, documented:** there is *no explicit high watermark* — performance fee is computed period by period with no memory of prior peaks.

## Product & data model

Where business language meets what the database actually stores.

- **Wallet** 🚩 — one custody account at one broker (unique on `(wallet_nix, broker)`). Carries the reconciliation policy and lock dates.
- **Aggregation** 🚩 — the consolidated view. *"Not a real financial entity — a logical filter defining which wallets/assets to include."* Built from wallet-split and asset-exclusion rules; its `is_fully_conciliated` property gates reporting.
- **Persona** 🚩 — the central registry entity, covering individuals and companies, and simultaneously client, prospect and banker. Known as the "persona god-table" internally, with a stated direction to break it apart.
- **Position vs. Movement** — a **Position** is a daily snapshot per `(date, asset, wallet)` carrying quantity, values, **PU** (unit price) and a battery of PnL/return windows. A **Movement** is an event (a trade). Movements flow `MovementInserter` → `MovementBooking` → `BrokerMovement`.
- **Conciliação** 🚩 — comparing the Nix side against the broker side, by type (`MOVEMENT` or `POSITION`). **It is not a line-by-line match**: the engine aggregates by key (`broker + wallet + asset + movement_type` per day) and compares totals — a documented risk, since it *"can mask offsetting trades."* Tolerance margin is configurable, default 0.25%.
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
- **Janela de cotação** — the secondary-market quotation window, Mon–Fri **10:00–15:00**. The most directly codifiable rule in the whole investments knowledge base.

## Where the knowledge base contradicts itself

Real, unresolved conflicts found while building this page. If you hit one, ask — don't pick a side silently.

- **Guardian / Guardião** — described in one place as a deterministic, LLM-free controller for agent-container lifecycle, and in another as a security layer filtering prompt injection. **These are not compatible.**
- **Bushido** — described as a reconciliation agent doing heavy mathematical validation in one document, and as an operational Nix executor / middle-office in more recent ones. The role probably evolved, but nothing says so.
- **3 Ondas vs. 4 Ondas** — both narratives live in the same market file; the 4-wave version declares that it replaces the 3-wave one. **Use the 4-wave version.**
- **"Nyx" vs. "Nix"** — one document writes the API as "Nyx"; everything else writes "Nix". Apparently a typo, worth confirming.
- **COI** — means *Certificado de Operações Estruturadas* (likely a transcription slip for COE) in a market context, and *Center of Influence* in an (archived) GTM context.

## Acronyms nobody has written down

Used across the knowledge base and code, never expanded anywhere. Listed so you know these are genuinely undefined rather than something you missed — worth asking about, and worth capturing here once answered.

`NIX` · `RPE` (highest-value unknown — appears in movement-sync services, forced-value statuses and an override endpoint) · `AUS` (the default `aggregation_type`, while a sibling config defaults to `AUM`, with no stated difference) · `PJ2` · `IPS` (`[inferred]` Investment Policy Statement) · `gross_up_value`

Standard market acronyms are treated as primitives and also never expanded: `CDI`, `IPCA`, `FGC`, `PDD`, `PL`, `B3`, `ANBIMA`.
