# How We Work — product & engineering process

How work is born, decided, specified and shipped at Revert. This is the answer to "I have
something to build — where do I start?"

**This section is a pointer, not a copy.** The process lives in one Notion page:

> **[Como Operamos — Engenharia & Produto](https://app.notion.com/p/Como-Operamos-Engenharia-Produto-3bfe07cf45c2800d83c9e5f331dda1fc)**
> (Notion: `Home → Best practices`) · owner: Taka · reviewed quarterly

Read it there. It's versioned by decision and revised every quarter, so a copy in this repo would
be wrong within a cycle — and the templates in it are meant to be copied from the live page, not
from a transcription. Everything below is a map to help you find the right part of it, plus the
context this repo can add.

## Why the process exists at all

Revert runs **without middle management**. That doesn't remove management — it moves it into
artifacts, metrics and cadence. The process doc is the artifact that replaces "go ask Matheus":
decisions happen at the right point, in writing, once.

The load-bearing consequence for you as an engineer: **leadership intervenes in the plan, not in
the execution.** A senior/STO reviews your Tech Spec in ~30 minutes — correcting course and
explaining the mental model, not just handing you the answer — and after that you build
autonomously. The pre-refinement ritual is what buys the autonomy.

## The shape of it

```
Iniciativa  →  PRD  →  Projeto  →  Tech Spec  →  Tarefas  →  Ship & Medir
(why)          (what)  (the slice) (the how)     (the step)  (the result)
```

**Notion is where you think** (PRD, Tech Spec — the *why* and the *how*, long text, discussion in
comments). **Linear is where you execute** (Initiative, Project, Issue — state, owner, date,
flow). Nothing is duplicated across the two; each pair links both ways.

**The chain rule.** Every task points to a project, which points to a PRD, which points to an
initiative, which points to a quarterly KPI. A broken link means the work shouldn't exist. If you
can't say that chain out loud, stop and fix that before writing code.

**Not everything needs all four artifacts.** The doc defines four tracks by risk — full (touches
money, or 2+ teams, or more than one cycle), short, direct, and incident. Process is a cost
justified by risk; read the track table before assuming you owe a PRD.

## What to look up where

| You need to know | Section of the doc |
|---|---|
| Which artifacts your work actually needs | §3 — Rigor escalonado (the four tracks) |
| What goes in a PRD, and when it's ready | §4 — PRD (Definition of Ready + template) |
| How to slice a project so it ships in ≤ 2 weeks | §5 — Projeto |
| How to write a Tech Spec, and who reviews it | §6 — Tech Spec |
| How small a task should be | §7 — Tarefas |
| Where a doc lives, and the double-link rule | §8 — Onde tudo vive |
| How to announce a cross-team change | §9 — Comunicação (`#engineering-changes`) |
| Whether you're about to make a known mistake | §10 — Anti-padrões |

## Where the documents live

Every PRD and Tech Spec sits under
[Home → Iniciativas](https://app.notion.com/p/Iniciativas-3b9e07cf45c280ed9935c52b3f2632de) in
Notion, inside its initiative — never in a personal space, a loose page, or a Slack attachment. If
it isn't there, it doesn't exist. The intended shape:

```
Iniciativas
└── <Team>                    Customer XP · Produto · Engineering · SRE & DevOps
    └── <Initiative>          e.g. "Middle com Escala"   ← links to the Linear Initiative
        ├── PRD — <name>
        │   └── Tech Spec — <project>
        └── Artefatos          research, analyses, taxonomies, direction docs
```

Create the initiative page in place, under your team's heading — don't create it loose and move it
later. An orphan page becomes a lost page.

> **The tree is still being populated** (read live 2026-08-17). Only **Customer XP** has real
> initiative pages so far — *Middle com Escala* and *Bruxo mais inteligente*. The remaining headings
> are deliberate placeholders (`Team 2`, `Team 3`) holding initiative names as plain text rather
> than pages, so Produto, Engineering and SRE & DevOps don't have their real headings yet. If your
> team isn't there, that's expected — create the heading and your initiative under it, following
> the shape above, rather than assuming you're in the wrong place.
>
> *Middle com Escala* is the one worked example to read before writing your first PRD. It holds
> `PRD — Middle Office em autopilot` and one artifact page (`Artefato - Fluxo de onboarding de
> investidor`) as direct children — note that the artifact sits beside the PRD rather than inside
> an `Artefatos` folder, and no Tech Spec exists under the PRD yet. Both are minor divergences from
> the shape above; follow the doc, not the example, where they disagree.

## Don't start from a blank page

Three Claude skills produce the drafts in the right format. They organize the reasoning; the
judgment — the slice, the appetite, the owner, what stays out of scope — stays human. A PRD
generated without field evidence is a pretty, empty PRD, and STO review will find that.

| To create | Skill |
|---|---|
| A **PRD** in Notion (from research, production data, customer conversations) | `prd-writer` |
| A **Project** in Linear (from a PRD, meeting, thread, brain dump) | `linear-project-writer` |
| **Issues** inside an existing project (from the project link) | `linear-issue-writer` |

The skills are configured in Claude, not in this repo — see the links in the process doc's §2.

## How this connects to the rest of this repo

- New to Revert entirely? Do the [Getting Started](../getting-started/README.md) conversations
  first. This section is about *how to build*; those are about *what we're building and for whom*.
  The process is much easier to follow once you know why the product exists.
- [Projects](../projects/README.md) — the live state of what's being built, in Linear.
- [Product & Architecture](../architecture/README.md) — the systems your Tech Spec will touch.
- [Glossary](../glossary/README.md) — domain vocabulary. Note that the *process* vocabulary
  (*apetite* P/M/G, *fatia vertical*, *pré-refinamento*) is defined in the Notion doc itself, not
  in the glossary. `STO` is used throughout the process without ever being expanded — the glossary
  lists it among the open acronyms; ask rather than guess.

## If Notion isn't reachable

Say so plainly and point the reader at the URL above. Don't reconstruct the process, the templates,
or the Definition of Ready lists from this page — this is a map, and it is deliberately not
complete enough to substitute for the source.
