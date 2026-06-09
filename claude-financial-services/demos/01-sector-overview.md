# Demo — Sector intel pack via Market Researcher (`sector-overview` skill)

**Agent**: `market-researcher`
**Skill**: `sector-overview`
**Surface**: Claude Cowork (personal instance)
**Target**: a public sector you choose. Worked example below uses **European banks**.

This demo produces a sector intel pack on a defined public-target sector: structure, key issuers, recent earnings season takeaways, regulatory backdrop, cross-issuer themes, and items flagged for analyst follow-up. The output is the kind of pack a senior associate would assemble in half a day; the demo runs in roughly 10 minutes interactive.

---

## Two ways to invoke

### Option A — let the agent orchestrate (recommended for the demo)

Just invoke `market-researcher` and describe the deliverable. The agent picks which of its skills to fire (it has five; for a sector pack it will lean on `sector-overview` as the spine and may call `competitive-analysis` on the issuers).

```
@market-researcher

Produce a sector overview pack on <SECTOR>. Use the sector-overview skill as
the primary structure. Cover: sector definition and segmentation, top
<N_ISSUERS> issuers, last earnings season cross-issuer themes, regulatory
backdrop, and 3–5 items flagged for analyst follow-up. Cite every claim.
End with a "what I assumed / what I could not verify" section.
```

### Option B — call the skill directly (more control, less natural for a demo)

Useful if you want to demonstrate skill-level addressability — but for an audience meeting Claude FS for the first time, Option A reads more naturally.

```
@market-researcher use skill: sector-overview

Target: <SECTOR>
Coverage depth: <SHALLOW | STANDARD | DEEP>
Issuers in scope: <LIST or "top N by market cap">
Time window for "recent": <last quarter | last 6 months | YTD>
Output format: <structured markdown | PPTX via pptx-author hand-off>
```

---

## Placeholders to fill

| Placeholder | What goes here | Example (European banks) |
|---|---|---|
| `<SECTOR>` | The sector definition. Be specific — vague sector = vague output. | "European banks — Eurozone-listed G-SIBs and large national champions, excluding pure-play asset managers and pure-play investment banks" |
| `<N_ISSUERS>` | How many issuers to cover in detail | 8 |
| `<TIME_WINDOW>` | Window for "recent" developments | "Q1 2026 earnings season (results released Apr–May 2026)" |
| `<REGULATORY_FOCUS>` | Regulatory threads you care about | "Basel III endgame implementation in EU vs UK; ECB SSM stress test results; MREL compliance progress" |
| `<THEMES_OF_INTEREST>` | Cross-issuer themes you want surfaced | "NII sensitivity to ECB cuts; CRE exposure runoff; capital return policies (buybacks vs dividends); cost-of-risk normalisation" |
| `<EXCLUSIONS>` | Things you do *not* want in scope | "No coverage of US or UK domestic-only banks; no private banks; no fintech challenger banks" |
| `<OUTPUT_FORMAT>` | What you want at the end | "Structured markdown intel pack, then ask whether to render via pptx-author for the desk" |

---

## Worked example — European banks, ready to paste

Pasted as-is, this gets you a credible first artifact in one turn. The 2–3 refinement turns after are where the demo gets interesting (insisting on stronger citations, pushing back on a thin section, asking for cross-issuer comparison tables).

```
@market-researcher

Produce a sector overview pack on European banks. Use the sector-overview skill
as the primary structure.

Scope:
- Eurozone-listed G-SIBs and large national champions (BNP Paribas, Santander,
  ING, UniCredit, Intesa Sanpaolo, Deutsche Bank, BBVA, Société Générale).
- Excluding: pure-play asset managers, pure-play investment banks, UK domestic
  banks, fintech challengers.
- Time window for "recent": Q1 2026 earnings season (results released April–May
  2026).

Deliverable structure:

1. Sector map — segmentation by business mix (retail / corporate / IB / wealth),
   geography, and balance-sheet shape.
2. Issuer cards — one per name above, ~6 lines each: business mix, key metric
   (P/TBV or P/E as appropriate), capital return policy, key thesis driver.
3. Q1 2026 cross-issuer themes:
   - NII sensitivity to ECB cuts (which banks guided what, who is most/least
     exposed)
   - CRE exposure and provisioning trajectory
   - Capital return policies — buyback announcements vs dividend changes
   - Cost-of-risk normalisation vs trough
4. Regulatory backdrop:
   - Basel III endgame implementation in EU (CRR3/CRD6 status)
   - ECB SSM stress test 2026 results, if released; if not, status
   - MREL compliance progress for the named issuers
5. Three to five items flagged for analyst follow-up — concrete things to chase
   (a disclosure to look for at the next quarter, a regulatory consultation
   closing soon, a deal rumour to verify).

Rules:
- Cite a source for every numeric claim and every quoted guidance figure
  (filing, transcript, press release, regulatory document). No claim without a
  citation.
- End with a "What I assumed / what I could not verify" section listing things
  you took a position on without a hard source.
- Output as structured markdown. After the artifact, ask whether to render the
  intel pack via pptx-author for the desk.
```

---

## Refinement turns to demonstrate in the talk

After the first-pass output, run at least two of these in front of the audience — they are where the capability becomes visible:

1. **Push back on a weak citation.**
   > "The NII sensitivity numbers in section 3 — give me the exact transcript page or slide number for BNP's and Santander's figures. Not the IR landing page; the document."

2. **Force a cross-issuer comparison table.**
   > "Build a table comparing the 8 issuers on: Q1 NII growth YoY, guided FY NII sensitivity to a –50bp ECB move, CET1 ratio, cost-of-risk in bps. One row per issuer. Cite each cell."

3. **Surface what is missing.**
   > "What did you have to skip because the source wasn't accessible or the data wasn't released yet? List those gaps explicitly — that's part of the deliverable."

4. **(Optional, if time permits) Hand off to `pptx-author`.**
   > "Render the intel pack as a PPTX via pptx-author. One slide per cross-issuer theme; the issuer cards as a 2-up appendix."

Each refinement turn demonstrates a different claim from `01-what-it-is.md`: citation discipline → source-attribution claim; cross-issuer table → structured-output claim; gap surfacing → "human-in-the-loop, honest about limits" claim; PPTX hand-off → M365 integration claim (via the `pptx-author` skill rather than the M365 plugin directly, but the audience sees the same shape).

---

## What to caveat at the start of the demo

Before running, say this to the room verbatim or close to it:

> "This runs in a personal Cowork instance. The sector is public — public companies, public filings, public earnings transcripts. The artifact you'll see is for demonstration. It's not produced with office tooling. It is not what would land in a sanctioned office deployment — the compliance and connector stack would be different. The point is to show *what the capability looks like at all*, not to show production output."

The caveat is the demo. Without it, the audience walks away thinking we already have this. We don't.

---

## What you are *not* demonstrating

Worth being explicit, since the audience may ask:

- **Not a real Excel model.** `sector-overview` produces an intel pack, not a workbook. If someone asks "can it build the model too?" — yes, the FS suite has `model-builder` for that, but it's a different skill and not what this demo exercises.
- **Not connector-grounded.** The personal Cowork instance does not have S&P / FactSet / LSEG connectors. The artifact uses public web sources, which is *worse* than what an enterprise deployment would do, not better.
- **Not auditable in the enterprise sense.** No SSO, no audit log, no retention policy. The artifact is honest about its sources, but the surrounding governance stack is the personal-tier one.

These three points are also the answer to the question "so why can't we just use it?" — they're the gap between personal tier and the sanctioned office deployment described in `02-how-it-ships.md` and `03-our-access-situation.md`.
