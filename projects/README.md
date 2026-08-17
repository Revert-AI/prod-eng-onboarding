# Projects

Current project status and active work live in **Linear**, not here — that content changes too fast
to keep a copy fresh in this repo. Fetch it live via the Linear MCP tool, every time.

## The teams

Verified live against the workspace on 2026-08-17:

**Engineering** · **Produto** · **Customer XP** · **SRE & DevOps** · **BUGS**

`BUGS` is for bugs only, and is the one place an issue is allowed to exist without a parent project.
The same four names (excluding `BUGS`) are also the team values used on Notion documents, so a PRD
and its Linear project agree on which team owns the work.

What each of the four actually covers is `Not yet documented — needs a human to fill in`. The names
are confirmed; the scope boundaries are not written down anywhere this repo could read. Note that
Customer XP and SRE & DevOps were both created in mid-August 2026, so they're new enough that the
split may still be settling — ask rather than inferring from what's currently in their backlogs.

> **Correction, 2026-08-17.** Earlier versions of this repo said Linear used a single team `REV`.
> That was wrong — it was written in a session where Linear was unreachable, and no such team
> exists. If you find `REV` referenced anywhere else, it's stale.

## How to read what you find there

The hierarchy is not flat, and the shape carries meaning:

```
Initiative        the ambition, tied to a quarterly KPI   → links to a PRD in Notion
└── Project       a shippable vertical slice, ≤ 2 weeks   → links to a Tech Spec in Notion
    ├── Milestone only when a project has 2+ marks
    └── Issues    tasks of ≤ 2 days
```

- A project's **Lead** is one named person, never a team. A project without a lead doesn't leave Backlog.
- **Status** is `Backlog → WIP → Completed`, and **WIP is capped at 3 per team**. A team at 3 isn't
  idle-capacity — a slot opens when something ships.
- **Target date** is the date that closes the appetite (P = 1 cycle, M = 2, G = 3), not an optimistic guess.
- `[DISCOVERY]` in a project name means the deliverable is an answer, not software.
- Issue state is moved by whoever executes, not by the project lead — so the board is meant to be
  trustworthy, and a stale board makes flow metrics useless.

Every project should link to its PRD and Tech Spec in Notion, and vice versa. If you have to ask
someone "where's the spec for this?", that double link failed — see
[How We Work](../how-we-work/README.md) for the rules these fields come from.

## If Linear isn't reachable

Say so plainly. Do not fabricate project status from commit history, this page, or anything else.
