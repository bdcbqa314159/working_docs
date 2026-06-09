# Beamer deck — build instructions

Same toolchain as the [Copilot pack](../../copilot-token-optimization/latex/) and the [Claude FS pack](../../claude-financial-services/latex/). If you've compiled either of those, this one needs nothing new.

## Compile

```bash
cd /Users/bernardocohen/work/desk_work/m365-sales-agent/latex
latexmk -pdf -xelatex m365-sales-agent.tex
```

Output: `m365-sales-agent.pdf` in this folder.

## Tectonic alternative

```bash
cd /Users/bernardocohen/work/desk_work/m365-sales-agent/latex
tectonic m365-sales-agent.tex
```

## Theme

Same Metropolis theme as the other two decks. **Teal accent** (`#0891B2`) — visually distinct from the Copilot deck (blue) and the Claude FS deck (purple), useful if you're presenting all three in the same session.

To change the accent: edit `\definecolor{accentteal}{HTML}{0891B2}` in the preamble.

## Source / single-source-of-truth

The deck content was written from scratch for the slide format (no `05-presentation.md` markdown equivalent in this pack — unlike the other two). If you edit the deck and want to keep it in sync with the markdown briefs, that's a manual step.

For the office talk, the .pdf produced from this .tex is the deliverable.
