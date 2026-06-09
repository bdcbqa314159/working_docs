# Claude for Financial Services — what it is, and where we stand

A briefing pack for the office on **Anthropic's Claude for Financial Services** offering: what it does, how it ships, and a direct, honest articulation of why we **cannot use it today** with our current toolset (Microsoft 365 Copilot + GitHub Copilot).

This pack is sister to the [Copilot token optimization pack](../copilot-token-optimization/). Same audience, same intent: give the team an accurate picture so they can plan around reality, not rumour.

---

## Why this pack exists

Anthropic announced **Claude for Financial Services** on 5 May 2026 — a packaged suite aimed squarely at the workflows our discipline cares about: pitchbooks, comps, DCFs, earnings reviews, KYC, GL reconciliation, NAV, month-end close. The release got significant industry attention; people on the floor are asking about it.

The honest situation:

- **Our office's AI access today**: Microsoft 365 Copilot + GitHub Copilot.
- **What we don't have**: any Claude subscription (no Claude Team, no Claude Enterprise, no Claude for M365 plugin, no Anthropic API access at the org level).
- **Implication**: the Claude for Financial Services agents are real and impressive, but they are **not available to us right now** through any sanctioned channel.

This pack helps the team understand:

1. What the Claude offering actually is (so we're not chasing hype or fiction).
2. What our current tools *can* do that overlaps with it.
3. What we *can't* do today, and what it would take to change that.

## Who this is for

Mixed audience: engineers, quants, PMs, analysts. The pack assumes financial-services familiarity but not Claude-specific familiarity.

## How to use this pack

| File | Read it if you want… | Time |
|---|---|---|
| [`01-what-it-is.md`](01-what-it-is.md) | The factual picture of Claude for Financial Services — agents, integrations, model | 10 min |
| [`02-how-it-ships.md`](02-how-it-ships.md) | Subscription tiers, deployment options, what unlocks what | 5 min |
| [`03-our-access-situation.md`](03-our-access-situation.md) | The honest articulation of our access reality | 5 min |
| [`04-what-we-can-do-today.md`](04-what-we-can-do-today.md) | Pragmatic guidance — what to do with the tools we have | 10 min |
| [`05-presentation.md`](05-presentation.md) | Pointer to the three PDFs (projection / handout / backup) — when to use which | — |
| [`latex/`](latex/) | Three LaTeX outputs — `*-minimal.pdf` (4 slides, projection), `*-handout.pdf` (2-page A4 leave-behind), `claude-financial-services.pdf` (16 frames, backup/reference) | — |
| [`narrative-script.md`](narrative-script.md) | Presenter script for the **minimal deck** — pre-read email, 4 anchor-slide cues, 7-min percussive monologue, 10-question Q&A facilitation | — |
| [`demos/`](demos/) | One concrete demo template (Market Researcher → `sector-overview`, public-target sector) | — |
| [`appendix-sources.md`](appendix-sources.md) | Every claim, where it came from | — |

## A note on the `demos/` folder

The user maintaining this pack has personal access to Claude.ai (consumer subscription). To make the capability tangible for an audience that has never seen Claude produce a financial deliverable, the `demos/` folder contains **prompt templates** to generate sample artifacts on public-information targets (e.g., a comps analysis on Microsoft, a DCF on Apple). These can be run in personal Claude and the outputs shown to the office.

**Important boundary**: nothing in `demos/` involves office data. The demos are pedagogical, not productive. Using personal Claude on office data would not be appropriate under our current data-handling posture, regardless of how interesting the output might be.

---

*Last verified: 2026-06-08 against `anthropic.com/news/finance-agents` and `github.com/anthropics/financial-services`.*
