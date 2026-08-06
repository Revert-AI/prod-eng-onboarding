---
last_verified: 2026-08-06
owner: TBD (repo maintainer — update to whoever owns this content)
---

# Org & Teams

Who owns what, and who to ask for a given context.

`last_verified` above applies to the static "Who owns what" section below. The **Leadership** section is a live pointer and carries no staleness date of its own — always fetch it fresh rather than trusting any cached read (see that section).

## Who owns what

No org chart or HR system was reachable when this section was written. What follows for the four product repos is **not** an authoritative org chart — it's a lightweight signal read off each repo's commit history (`git log --format='%an <%ae>' | sort | uniq -c | sort -rn`, most recent ~200 commits per repo, full history where a repo has fewer). Treat it as "who's touched this most recently, as best we can tell from git," not "who owns this." A human should confirm before relying on it. None of the four repos has a `CODEOWNERS` file or a README section naming an owning team, so commit history is the only signal available.

A recurring caveat: several contributors appear under two or more identities in the same repo (e.g. a GitHub-noreply username alongside a personal name/email) — the counts below are per identity string as git recorded it, not de-duplicated across aliases, so a single person's real total may be understated.

- **`nix_webserver`** — Commit history suggests `guiscan` has been the most frequent recent contributor (63 of the last 200 commits), followed by `danielrevertai` (31) and `ehbats` (25). Unconfirmed — ask them or your onboarding contact to verify.
- **`portal_v2`** — Commit history suggests `guilherme.scagnolato` has been the most frequent recent contributor (353 of the last ~1,300 commits visible), with `Jardel Ferreira`/`Jardel Gonçalves` and `Guilherme Carneiro`/`guiscan` also frequent (the latter two pairs may each be one person under two identities — unconfirmed). Ask them or your onboarding contact to verify.
- **`concierge-agent-pi`** — Commit history suggests `Yuri Brito` (appearing as both `yuri.brito` and `yuribrito-revai`) has been the primary contributor (117 + 84 commits across those two identities). Unconfirmed — ask them or your onboarding contact to verify.
- **`revert-cloud-infra`** — Commit history suggests `Matheus Cruz` (`mathmedcruz`) has been essentially the sole contributor (27 of 28 total commits in the repo's full history). Unconfirmed — ask them or your onboarding contact to verify.

For anything not covered above — team structure, functional groups (e.g. who's on growth, sales, support), reporting lines, or who to ask about a topic that isn't one of the four repos — `Not yet documented — needs a human to fill in`. Whoever owns this file should replace this note and the inferred signals above with a confirmed map, and update `last_verified`.

## Leadership

Founder and leadership bios are **not** duplicated in this repo. For that, consult `revert-knowledge-base` live, every time — don't rely on a cached read of this file for anything leadership-related:

1. Clone with `git clone --filter=blob:none --no-checkout <remote>` into a scratch directory outside this repo's working tree.
2. Run `git sparse-checkout set "company/about revert/team/"` — that path only.
3. That folder is an index of individual leadership/founder profiles (CVs) — read it live to answer any question about who the founders/leadership are and their backgrounds.

Do not fetch, list, or reach any other path in `revert-knowledge-base` from this section (in particular `company/fundraising/`, `sales/`, `regulation/`, and `company/atas/` are always off-limits — see `AGENTS.md`). If `revert-knowledge-base` isn't reachable, say so plainly rather than answering from anything else — this section has no static fallback content.
