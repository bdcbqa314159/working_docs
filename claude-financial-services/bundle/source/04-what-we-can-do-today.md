# 4. What we can do today — pragmatic guidance with the tools we have

The access situation in `03` is the reality. This file is about working well within it. Three angles: where M365 Copilot earns its keep for FS work, what we can borrow from the open-source Claude FS repo without subscription access, and what role personal Claude can legitimately play.

## Angle 1 — M365 Copilot is more useful for FS than people give it credit for

M365 Copilot is often dismissed because it isn't Claude. That's the wrong comparison. The right comparison is: **what FS-flavoured tasks does it actually do well today?**

### Where M365 Copilot is genuinely strong

| Task | Surface | Why it works |
|---|---|---|
| Drafting client emails / cover notes | Outlook | Native context: prior thread, CRM if integrated, recipient signals |
| Summarising long meetings | Teams | Live transcript, speaker attribution, action-item extraction |
| Summarising SharePoint document trees | M365 Copilot Chat | Native indexing — no upload needed |
| Comparing two versions of a deck | PowerPoint | Cross-file diff with context |
| Building a first-cut model from a spec | Excel | Copilot in Excel can scaffold from a written description |
| Sensitivity analysis on existing models | Excel | "Vary X by ±10% and show me Y" works well |
| Drafting commentary on existing dashboards | Excel / Power BI | Reads the data, writes the narrative |
| Reconciling against Dynamics 365 or SAP | Copilot Studio agents | Connectors to the firm's ERP if installed |
| First-pass summarisation of a credit memo | Word | With the document open, summarise + flag issues |

The pattern: **anything that lives inside the M365 surface and benefits from knowing what's around it**. That's a non-trivial chunk of analyst work.

### Where M365 Copilot is weak for FS

Equally honest:

| Task | Why Copilot struggles |
|---|---|
| Building a model from a filing | Reading and structuring 10-K data is reasonable; complex modelling reasoning is not its strength |
| Multi-doc synthesis across 200 pages | Limited useful context; degrades on long inputs |
| Source attribution on every claim | Inconsistent; sometimes attributes, sometimes doesn't |
| Pulling from FactSet / S&P / PitchBook directly | No native connectors; you'd manually paste data |
| Running an autonomous multi-step workflow | Copilot Studio agents exist but require building; not pre-baked for FS |
| Complex Excel auditing (formula-chain reasoning) | Improving, but still below Claude/Opus on FMW-style tasks |

**Implication**: when you have the choice, **route the task to the surface that fits**. Don't try to make Copilot do a thing it's bad at when a different approach (manual + Copilot's good lane, or a different tool entirely) does it better.

## Angle 2 — Read the open-source FS repo even without access [4]

Even without subscription access, the **[anthropics/financial-services](https://github.com/anthropics/financial-services) repo** is a legitimate resource. It's Apache 2.0 and contains:

- **Skill markdown files** — the actual written instructions Anthropic's FS team gave each agent. These read like senior-banker SOPs. Worth reading for the *task structure* alone, independent of any AI.
- **Slash command definitions** (`/comps`, `/dcf`, `/earnings`, `/ic-memo`, etc.) — each defines what inputs the task needs, what intermediate steps to run, and what output format to produce.
- **`agent.yaml` cookbooks** — show how Anthropic structures multi-step agents (when to call which subagent, where to insert human review checkpoints).

**What we can take from it**:

1. **Workflow templates we can adopt for our own SOPs.** If our team is documenting a pitchbook-building process, the open-source `pitch-agent` skill is a reasonable reference for "what does a thorough one look like, written down".
2. **A view of where the industry is heading on AI-augmented FS workflows.** Worth being literate about — it's where future tooling decisions will be made.
3. **A starting point if we ever do get API access.** Forking and adapting is cheaper than building from scratch.

What we **cannot** take from it: a way to run the agents without an Anthropic-account-backed Claude. The cookbooks orchestrate Claude API calls. Without an API key (and the org-level permission to use one), the cookbooks are reference material, not runnable software.

## Angle 3 — Personal Claude has a narrow but legitimate role: demonstration

The boundary from `03` stays firm: **personal Claude is not for office data**. But it does have a legitimate role for **showing the audience what's possible** using public-information targets.

This is what the [`demos/`](demos/) folder is for. The idea:

- Pick a publicly-known company (e.g. Microsoft, Apple, a recent IPO).
- Use Claude.ai or Claude desktop to run a workflow (DCF, comps, earnings review) using **only public data** (10-Ks, earnings transcripts, press releases).
- Save the output (the model, the deck, the memo) as a **show-and-tell artifact** for the office presentation.

What this accomplishes:

1. Makes "Claude can build a DCF in PowerPoint" *visible* rather than asserted. Audiences respond to seeing the artifact.
2. Stays cleanly inside the data-handling boundary (no office IP touched).
3. Gives us a felt benchmark for what we'd gain (or wouldn't) from sanctioned access.

What this does NOT accomplish:

- It does not constitute "using Claude for FS at the office". The demo is pedagogy.
- It does not substitute for production capability — the production environment we'd need (audit, retention, SSO, FS data connectors) doesn't exist in personal Claude.

### Doing the demos responsibly

Three rules for any artifact in `demos/`:

1. **Only public-information targets.** Listed companies, public filings, public press releases. No private deal data, no client names, no internal documents.
2. **Annotate the artifact** — at the top of every generated document, note "Generated via personal Claude account on public data, for demonstration only. Not produced using office tooling or office data."
3. **Do not store the artifact alongside actual office work.** Keep demos in this `demos/` folder; do not mix them into project deliverables.

The prompt templates in [`demos/`](demos/) are designed with these rules baked in.

## Quick decision table — what tool for which FS task today

| Task | Best with what we have |
|---|---|
| Draft a client email summarising a meeting | M365 Copilot (Outlook + Teams transcript) |
| Build first-cut LBO model from a written spec | M365 Copilot in Excel; manually fill any data |
| Run sensitivity on an existing model | M365 Copilot in Excel |
| Summarise a 50-page credit memo | M365 Copilot in Word (with file open) |
| Read 4 earnings transcripts, identify thesis-relevant shifts | M365 Copilot is weak here. Manual review + Copilot to draft the writeup once you've decided what matters. |
| Build a pitchbook with comps + DCF | Build the model + slides yourself; use M365 Copilot to draft narrative, format, sense-check |
| Pull comps from FactSet into Excel | Use FactSet directly (no AI in the loop); Copilot to help shape the comparison |
| Write a Python script to ingest a feed | GitHub Copilot |
| Code review on a notebook | GitHub Copilot Chat |

The implicit principle: **do the AI-leveraged steps where the AI is strong; do the steps it isn't strong at the regular way**. That's how to extract real value from M365 + GitHub Copilot today without overreaching.

---

## Sources

[4] GitHub — *anthropics/financial-services repository* (Apache 2.0 templates, skills, MCP connectors). <https://github.com/anthropics/financial-services>
[12] Microsoft — *Compare Copilot vs. Claude Enterprise.* <https://www.microsoft.com/en-us/microsoft-365-copilot/copilot-vs-claude-enterprise>
[13] Ninetwothree — *Claude vs. Microsoft Copilot for Excel.* <https://www.ninetwothree.co/blog/claude-vs-microsoft-copilot-for-excel>

---

Next: [`05-presentation.md`](05-presentation.md) — Marp slide deck for an office briefing.
