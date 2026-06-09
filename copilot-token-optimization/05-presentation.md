---
marp: true
theme: default
paginate: true
size: 16:9
header: 'Copilot Token Optimization · Internal · June 2026'
footer: 'For team use — verify pricing before procurement decisions'
style: |
  section { font-family: 'Inter', 'Helvetica', sans-serif; padding: 60px; }
  h1 { color: #1f2937; border-bottom: 3px solid #2563eb; padding-bottom: 12px; }
  h2 { color: #1f2937; }
  table { font-size: 0.85em; }
  code { background: #f3f4f6; padding: 2px 6px; border-radius: 4px; }
  .small { font-size: 0.8em; color: #6b7280; }
  .big { font-size: 1.4em; font-weight: 600; color: #2563eb; }
  .columns { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; }
---

# GitHub Copilot
## Token Optimization Under the New Billing

How to keep our Copilot productivity without burning through our AI Credits

<br>

*Internal session — 20 minutes + Q&A*
*June 2026*

---

## What changed on 1 June 2026

- The old system: **one chat turn = one "premium request"**, multiplied by a per-model factor. Plans gave us **N requests / month**.
- The new system: plans give us a **dollar budget in AI Credits**. Every paid surface bills against it **by tokens × per-model rate**.

<br>

> **1 AI Credit = \$0.01**
> **Code completion + Next Edit Suggestions are still free.**
> **Chat, Edit mode, Agent mode, Code Review are paid.**

---

## Why this matters

A realistic Agent-mode session on Opus can spend **\$0.50 to \$5+** in credits.

Public reports document developers burning **\$30–40 in a single morning's session**.

Pro is **\$10/month**. The math is unforgiving if we're not deliberate.

<br>

The good news: **the highest-frequency Copilot interactions — completion and NES — remain unmetered**. Most of the productivity we get from Copilot is in the free lane.

---

## The plan allowances

| Plan | Monthly cost | Monthly AI Credits |
|---|---|---|
| Copilot Pro | \$10 | \$10 |
| Copilot Pro+ | \$39 | \$39 |
| Copilot Business | \$19 / seat | \$19 / seat |
| Copilot Enterprise | \$39 / seat | \$39 / seat |

No rollover. Overage billable per-token (admin policy applies).

---

## The five surfaces in VS Code

| Surface | Bills? | Typical cost |
|---|---|---|
| **Code completion** (ghost text) | No | Free |
| **Next Edit Suggestions** | No | Free |
| **Chat — Ask** | Yes | Small per turn |
| **Chat — Edit** | Yes | Medium — whole file in & out |
| **Chat — Agent** | Yes | **Largest** — tool output stacks |
| Code Review (PR / inline) | Yes | Per review, ∝ diff size |

---

## Where the tokens come from

On every paid turn:

```
cost = (your prompt + attached context + chat history + tool output history) × input_rate
     + (model's reply + new tool calls) × output_rate
```

<br>

Four controllable levers, in priority order:

1. **Which model** (cheapest vs most expensive: ~10× spread)
2. **Tool output history** (agent mode — dominates)
3. **Attached context size** (`#selection` vs `@workspace` vs dragged folder)
4. **Chat history length** (new chat per topic)

---

## Lever 1 — Model selection

The **single highest-leverage decision** you make per turn.

| Tier | Examples | When |
|---|---|---|
| Cheap | Haiku 4.5, GPT-5 mini, Gemini 3 Flash, GPT-5.4 nano | Exploration, summarising, simple edits |
| Standard | Sonnet 4.6, GPT-5.4, Gemini 3.1 Pro | Multi-file edits, careful implementation |
| Premium | Opus 4.7, GPT-5.5 | Hard reasoning, deep debugging, architecture |

<br>

**Action**: in VS Code, set your default model to a **cheap-lane** model. Escalate deliberately.

---

## The two-lane workflow

```
EXPLORE  →  Cheap lane (Haiku, GPT-5 mini)
            ask · plan · summarise · iterate freely
                        │
                        ▼
EXECUTE  →  Premium lane (Sonnet+ / Opus)
            one well-formed implementation turn
                        │
                        ▼
VERIFY   →  Cheap lane again
            review the diff · write tests · ask "does this look right?"
```

<br>

The framing: **expensive models for executing locked decisions; cheap models for exploring undecided ones.**

---

## Lever 2 — Context size

Token cost ranking (cheapest → most expensive):

```
#selection   <   #editor   <   #file:<name>   <   @workspace / #codebase   <   dragged folder
```

<br>

Rules:

- 20 lines matter → `#selection` them, don't attach the file.
- One file matters → `#file:` it, not `@workspace`.
- `@workspace` is for "I don't know which files matter yet."
- **Never drag a folder in** unless that's truly the intent.

---

## Lever 3 — Conversation hygiene

**Anti-pattern — prompt-chipping:**

```
"Refactor this to use a dict."
"Actually use defaultdict."
"Make the keys strings."
"Add type hints."
```

Four turns, four bills, each carrying the whole history.

<br>

**Pattern — one complete brief:**

```
"Refactor this to use a collections.defaultdict[str, list[Foo]],
 add type hints, keep the existing public signature."
```

---

## Lever 4 — Agent mode discipline

Agent mode is where the budget vanishes if you're casual.

**Front-load the brief**:

- **Task** — one sentence
- **In scope** / **Out of scope** — which files; what NOT to touch
- **Constraints** — patterns to preserve, libs required/forbidden
- **Definition of Done** — how the agent knows to stop
- **Reporting** — summarise files touched + assumptions

<br>

A well-shaped brief routinely **cuts agent sessions from 20 turns to 4–6**.

---

## Watch the token counter

The chat panel shows token usage in the **bottom-right corner**.

| Tokens in context | What to do |
|---|---|
| Under 30K | Comfortable, continue |
| 30–80K | Expensive on premium models — consider whether you're going in circles |
| 80K+ | Stop. Summarise to a fresh chat. |

---

## Repo-level reusable context

Stop re-pasting "remember, we follow X convention". Put it in a file Copilot auto-loads.

<br>

**At repo root** — `.github/copilot-instructions.md`:

```markdown
- We use Python 3.12, type hints required.
- No bare `except`. Use specific exceptions.
- SQLAlchemy 2.x — no `Query` API; use `select()`.
- Tests in `tests/`, one test file per source module.
```

<br>

**For repeated task shapes** — `.github/prompts/<name>.prompt.md`:
reusable templates for "write tests in our style", "refactor to our pattern", etc.

---

## Quick wins — adopt this week

- [ ] **Default model** → Haiku 4.5 or GPT-5 mini in VS Code chat
- [ ] **Bind a shortcut** → "New Chat" for one-keystroke restart
- [ ] **`.github/copilot-instructions.md`** in every active repo
- [ ] **Stop using drag-folder** entirely; always `#file:` or `@workspace`
- [ ] **One brief, not four chips** — write the full prompt
- [ ] **Glance at the token counter** before big turns

---

## What we're trading

These habits feel like upfront work.

The trade is **upfront thinking vs. downstream burn**:

| | Cost |
|---|---|
| Writing a complete prompt | +1 min thinking |
| Switching models mid-task | +5 sec clicks |
| Starting a new chat per topic | +2 sec |

In exchange:

| | Effect |
|---|---|
| Credit burn | **−50% to −80%** typical |
| Output quality | Usually meaningfully better |
| Need to redo work | Lower |

---

## Summary — the five rules

1. **Free is free** — completion + NES don't bill. Default to them whenever shaped like "complete this".
2. **Cheap model first** — explore on Haiku / mini; escalate only to execute a locked plan.
3. **Attach less** — `#selection` before `#editor` before `#file:` before `@workspace`.
4. **One task = one chat** — new chat per topic change.
5. **Agent mode = high-stakes mode** — front-load the brief, set Definition of Done.

---

## Resources we maintain

Everything in this talk is documented in the team repo:

- `README.md` — the overview and how to use the pack
- `01-new-billing-model.md` — the billing system, allowances, model rate card
- `02-vscode-surfaces.md` — per-surface deep dive
- `03-optimization-playbook.md` — the full playbook
- `04-cheatsheet.md` — one-page printable reference
- `appendix-sources.md` — every claim, where it came from

<br>

*Questions?*
