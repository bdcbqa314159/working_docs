# Beamer deck — build instructions

This folder contains the LaTeX (Beamer / Metropolis theme) version of the office presentation. Source: `copilot-token-optimization.tex`. Target: `copilot-token-optimization.pdf` (~19 slides, 16:9).

The deck uses the **Metropolis** theme which renders best with **XeLaTeX** or **LuaLaTeX** because it uses the **Fira Sans** font family. It will also compile under `pdflatex` with default fonts as a fallback.

---

## Option A — Recommended: MacTeX (full distribution, ~5 GB)

The simplest path. Installs everything we need, including Metropolis, Fira, and all standard packages.

```bash
brew install --cask mactex-no-gui
```

`mactex-no-gui` is MacTeX without the GUI apps (TeXShop, BibDesk, etc.) — saves ~500 MB. If you want the GUIs, use `mactex` instead.

After install, **open a new terminal** so the PATH picks up `/Library/TeX/texbin`. Verify:

```bash
which xelatex latexmk
```

Both should resolve.

### Compile

```bash
cd /Users/bernardocohen/work/desk_work/copilot-token-optimization/latex
latexmk -pdf -xelatex copilot-token-optimization.tex
```

`latexmk` runs as many passes as needed to resolve all references. Output is `copilot-token-optimization.pdf` in this same folder.

To clean intermediate files:

```bash
latexmk -c
```

To clean everything including the PDF:

```bash
latexmk -C
```

---

## Option B — Lighter: BasicTeX + manual packages (~150 MB)

Smaller install but you'll fetch missing packages manually with `tlmgr`.

```bash
brew install --cask basictex
```

Open a new terminal, then:

```bash
sudo tlmgr update --self
sudo tlmgr install latexmk beamer beamertheme-metropolis pgfopts \
                   fontspec fira microtype booktabs listings xcolor \
                   hyperref babel-english
```

Then compile the same way:

```bash
cd /Users/bernardocohen/work/desk_work/copilot-token-optimization/latex
latexmk -pdf -xelatex copilot-token-optimization.tex
```

If the build complains about a missing package, install it with:

```bash
sudo tlmgr install <package-name>
```

---

## Option C — Lightest: Tectonic (~30 MB, modern engine)

Tectonic is a self-contained LaTeX engine that downloads packages on demand. Cleanest for one-off builds.

```bash
brew install tectonic
```

Compile:

```bash
cd /Users/bernardocohen/work/desk_work/copilot-token-optimization/latex
tectonic copilot-token-optimization.tex
```

First run will download the packages it needs (Metropolis, Fira, beamer, etc.) — takes ~30 seconds. Subsequent runs are fast and cached.

Tectonic uses XeLaTeX semantics by default, which matches what this deck wants.

---

## If you don't want to install anything locally

Upload `copilot-token-optimization.tex` to **Overleaf** (free account) and compile there. Overleaf has Metropolis pre-installed; just set the compiler to **XeLaTeX** in the project settings (Menu → Compiler → XeLaTeX).

---

## Editing tips

- Slide content lives in `\begin{frame}...\end{frame}` blocks. The order in the `.tex` file is the order in the deck.
- The `\hl{...}` macro renders text in the accent blue, bold. Use it for key terms.
- The `\good` and `\bad` macros produce a green checkmark and a red cross — useful in tables.
- Sections (`\section{...}`) produce a divider slide automatically because of the `sectionpage=progressbar` theme option.
- To change accent colour: edit `\definecolor{accentblue}{HTML}{2563EB}` in the preamble.
- Aspect ratio is set in `\documentclass[...,aspectratio=169]{beamer}`. Use `aspectratio=43` for 4:3 if you're presenting on an older projector.

---

## If the build fails

Common issues and fixes:

| Error | Fix |
|---|---|
| `! LaTeX Error: File 'beamerthememetropolis.sty' not found.` | Install `beamertheme-metropolis` via `tlmgr install beamertheme-metropolis` (Option B) or just use MacTeX (Option A). Tectonic will fetch it automatically. |
| `! Fontspec error: 'font-not-found'` | The Fira font isn't on your system. Either install Metropolis as above, or switch the compiler to `pdflatex` (will use Computer Modern — looks less polished but works). |
| `! Package pgfkeys Error: I do not know the key '/metropolis/...'` | `pgfopts` package missing; install with `tlmgr install pgfopts`. |
| Compile succeeds but Metropolis looks plain | You compiled with `pdflatex` instead of `xelatex`. Use `latexmk -pdf -xelatex ...` |
