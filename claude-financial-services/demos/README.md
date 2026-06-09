# Demo — one concrete artifact for the office talk

This folder contains **one** demo: a prompt template you can run in **Claude Cowork** against the **Market Researcher** FS agent (skill: `sector-overview`) on a **public-target sector**. The output is a sector intel pack — concrete enough that the audience leaves understanding *what Claude for Financial Services actually does*, not just what it's marketed as.

One demo, deliberately. The previous version of this folder had seven; that was a presentation problem, not a richness problem. Three demos in a 20-minute talk means none of them lands.

## Boundary — read before running

1. **Public targets only.** Public companies, public filings, public press releases, public broker research where licensing permits. No private deal data, no client names, no internal documents.
2. **Annotate the output** at the top:
   > *Generated via personal Cowork instance on public data, for office demonstration only. Not produced using office tooling or office data.*
3. **Don't mix this artifact into project deliverables.** Demo lives in this folder; production work does not.
4. **Don't represent the demo as production capability.** What runs in a personal Cowork instance on public data is not what would run in a sanctioned office deployment. The demo shows *direction*, not *deliverable quality at our compliance standard*.

## The demo

| File | What it demonstrates | Target | FS agent / skill |
|---|---|---|---|
| [`01-sector-overview.md`](01-sector-overview.md) | Sector intel pack — cross-issuer synthesis from filings, transcripts, broker research | European banks (worked example) | `market-researcher` → `sector-overview` |

Why this one:

- **It exercises the three claims** the pack makes about Claude FS — long-context document synthesis (multiple filings + transcripts), structured output (the intel pack format), source attribution (every claim cited).
- **It's a category the audience recognises** — every desk consumes sector intel packs in some form.
- **It maps cleanly to one FS skill**, so the demo is honest about which capability it's exercising. No category drift.

## How to run it

1. Open Claude Cowork.
2. Invoke `market-researcher` (the agent), targeting the `sector-overview` skill specifically — see the template for the exact invocation pattern.
3. Paste the template; fill the placeholders; iterate 2–3 turns.
4. Export the artifact (PDF/PPTX via Cowork artifacts, or structured Markdown).
5. Add the annotation header above.

## What good looks like

A well-run sector intel demo:

- **Cites a source for every claim** (filing, transcript, press release, broker note). Insist on this; reject paragraphs without citations.
- Ends with a **"what I assumed / what I couldn't verify"** section.
- Looks like an **artifact** (downloadable document), not a chat transcript.
- Holds up to a "would I send this to a PM" sniff test — not in compliance, but in shape.
