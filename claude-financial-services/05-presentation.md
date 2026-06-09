# 5. Presentation

Three PDFs live in `latex/`. Each has one role.

## The three artifacts

| File | Pages | Role |
|---|---|---|
| **[`latex/claude-financial-services-minimal.pdf`](latex/claude-financial-services-minimal.pdf)** | 4 anchor slides | **Projection.** What you click during the talk. Small-room (≤12) hybrid delivery — screen off most of the time, slides up only at the four cues in `narrative-script.md`. |
| **[`latex/claude-financial-services-handout.pdf`](latex/claude-financial-services-handout.pdf)** | 2-page A4 | **Leave-behind / drill-by-themselves.** The audience takes this away. Headline + 10 agents + 3 ship paths + have/don't (page 1); colleagues script + personal-accounts callout + 10-question FAQ + further reading (page 2). Printable; works in B&W. |
| **[`latex/claude-financial-services.pdf`](latex/claude-financial-services.pdf)** | 16 frames (21 PDF pages incl. metropolis section dividers) | **Backup / reference.** Use as the delivery deck if the room is medium/large or remote/hybrid; otherwise send to anyone who asks for "more depth" after the session. |

All three share the same colour palette and core content. The minimal deck and handout are subsets of the full deck.

## Compile

From this directory:

```sh
cd latex

# Minimal deck (4 anchor slides for projection during the talk)
latexmk -pdf -xelatex claude-financial-services-minimal.tex

# Handout (2-page A4 leave-behind for the audience)
latexmk -pdf -xelatex claude-financial-services-handout.tex

# Full deck (16 frames as backup / reference)
latexmk -pdf -xelatex claude-financial-services.tex
```

Outputs: `claude-financial-services-minimal.pdf`, `claude-financial-services-handout.pdf`, `claude-financial-services.pdf`.

## Present from

- **The PDF** (any PDF viewer in presentation mode — or just open on the laptop facing the table in a small-room session).
- **The script**: [`narrative-script.md`](narrative-script.md) — the script is currently written against the **minimal deck**. If you switch to the full deck, retrieve the prior slide-number-keyed version from git history.

## Slot guidance

| Format | Deck | Slot | Mix |
|---|---|---|---|
| **Small-room percussive (≤12, current narrative-script.md)** | Minimal (4 slides) | 30 min total | **~7 min monologue, ~20 min discussion** |
| Small-room extended (≤12, prior version of script) | Minimal (4 slides) | 25–30 min | ~12 min monologue, ~15 min discussion |
| Medium-room talk (12–30 people) | Full (16 frames) | 20 min + 10 min Q&A | ~17 min monologue, ~10 min Q&A |
| Large-room / hybrid / remote | Full (16 frames) | 20 min + Q&A | Same as medium-room; visuals carry more weight |

The **current** `narrative-script.md` targets the percussive 7-min variant. If you switch to the extended 12-min version, retrieve the prior script from git history.

## If you need Marp / HTML / Keynote

The pack does not ship a Marp version. If you must present from Marp/HTML or convert to Keynote, regenerate from the LaTeX content rather than maintaining a second deck. The talking points in `narrative-script.md` are independent of the rendering surface — the four "bring up anchor slide N" cues map cleanly to whatever rendering you use.
