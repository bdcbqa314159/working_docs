# 3. The optimization playbook

This is the operational core of the pack. Eleven anti-patterns to stop, eleven habits to adopt, organized by the lever they pull.

If you read nothing else, read the **"Five-minute version"** below.

---

## The five-minute version

1. **Free is free** — code completion + Next Edit Suggestions don't bill. Default to them whenever the task is shaped like "complete this code".
2. **Cheap model first** — for exploration, brainstorming, "is this right?" turns, use a small model (Haiku 4.5, Gemini 3 Flash, GPT-5.4 nano, Raptor mini). Switch to a premium model only when the task is "implement the locked-in plan."
3. **Attach less context** — `#selection` before `#editor` before `#file:` before `@workspace`. Never drag a folder in unless you mean it.
4. **One task = one chat** — start a new chat when the topic changes. Long-running chats inflate every subsequent turn's input.
5. **Agent mode = high-stakes mode** — front-load the brief, set a clear definition of done, and don't re-purpose a stale agent session.

The rest of this file is detail and worked examples.

---

## Lever 1 — Model selection

The cost spread between models is roughly **10–40×**, and the *quality* spread on routine coding tasks is often **negligible**. This is the single highest-leverage lever.

### The four tiers

| Tier | Models (representative) | When to use |
|---|---|---|
| **Free lane** | Code completion, NES (built-in) | Anytime the cursor is in code |
| **Cheap chat** | GPT-5.4 nano, Raptor mini, GPT-5 mini, Gemini 3 Flash, Haiku 4.5 | Exploration, "what does this do", small refactors, summarizing, planning |
| **Standard chat** | GPT-5.4, GPT-5.4 mini, Gemini 3.1 Pro, Sonnet 4.6, MAI-Code-1-Flash | Multi-file edits, code review of a tricky diff, careful implementation |
| **Premium chat** | GPT-5.5, Opus 4.7/4.8, Gemini 3.1 Pro (>200K), GPT-5.4 (>200K) | Hard reasoning, architectural decisions, debugging across a large codebase |

### The two-lane workflow [6]

Adopted from community optimization guides — the strongest single habit you can build:

1. **Open chat in cheap-lane model** (Haiku 4.5 or GPT-5 mini are sensible defaults).
2. **Explore the problem**: ask "what's this code doing", "what are my options", "draft a plan to do X". Iterate freely — these turns cost a few credits each at worst.
3. **Lock the plan** — once you and the cheap model have agreed on a concrete plan, copy that plan into a new chat.
4. **Switch to the standard or premium lane** — and ask only the implementation question, with the plan pasted in. This is your one expensive turn.
5. **Verify back in the cheap lane** — code review, test edits, "does this look right?" go back to cheap.

The framing: **expensive models for executing locked decisions; cheap models for exploring undecided ones**. Reversing this is the most common way to burn the budget.

### Setting your default model

In VS Code: click the model picker in the chat panel input area → pick a default. For most people, **set the default to a cheap-lane model** (e.g. Haiku 4.5 or GPT-5 mini). Reach for premium models deliberately, not by accident.

### Anti-pattern: "Is this right?" on Opus

Asking a one-sentence confirmation ("does this look correct?") on an Opus model burns 15–25K input tokens (your code + history) at \$5/M and a few hundred output tokens at \$25/M. That's 10–15 credits for a yes/no. Do these on a cheap-lane model — or better, just look at the code yourself.

---

## Lever 2 — Context attachment

Every token of context is **paid input** on every turn it stays in the conversation. The default should be to attach the **minimum** context needed to answer the question.

### The cheapest → most expensive ranking

```
typed code in prompt   <   #selection   <   #editor   <   #file:<name>   <   @workspace / #codebase   <   dragged folder
```

### Rules of thumb

- If the answer hinges on **20 lines**, paste those 20 lines (or `#selection` them) instead of the whole file.
- If the answer hinges on **one file**, use `#file:<name>` or `#editor` — not `@workspace`.
- `@workspace` is great when you genuinely don't know which files matter; it's wasteful when you do.
- **Never drag in a folder** unless you want every file in it sent. The token cost can be 10–100× what you wanted.

### Reusable context lives in files, not chats [6]

If you find yourself re-pasting "remember, we follow snake_case, we use SQLAlchemy 2.x, we don't use bare except" into every chat, move that into a **persistent instructions file**:

- Create `.github/copilot-instructions.md` at the repo root.
- Add your team's coding conventions, library choices, and gotchas.
- Copilot auto-loads it on every chat in that repo. The cost is amortized: you write it once, and although those tokens *are* included in every turn's input, they're often eligible for **cached input pricing** (10× cheaper than fresh input [2]), and you don't re-type them — which means fewer overall turns spent re-explaining.

Same idea for repeated task patterns: drop `.prompt.md` files in `.github/prompts/` for things like "write unit tests for the selected function in our test style" and invoke them as one-liners.

### Anti-pattern: chat history bloat

Every turn of the current chat is replayed as input on the next turn. A 20-turn chat where each turn has 5K of context is sending **100K input tokens on turn 21**. That's \$0.30 input on Sonnet, \$0.50 on Opus — for one turn.

**Fix**: when you change topic, start a **new chat** (`+ New Chat` icon in the panel). When you continue a task across days, paste a 3-bullet summary of "decisions so far / next step" into a fresh chat and discard the old one.

---

## Lever 3 — Conversation hygiene

These habits stretch a given model + context budget across more actual work.

### Keep one good prompt going (don't fragment)

Anti-pattern (called "prompt-chipping" in optimization literature [6]):

```
Turn 1: "Refactor this to use a dict."
Turn 2: "Actually use defaultdict."
Turn 3: "Make the keys strings."
Turn 4: "Add type hints."
```

Each turn is a full request with the whole prior context. Four turns = four bills.

Better:

```
Turn 1: "Refactor this to use a collections.defaultdict[str, list[Foo]],
         add type hints, and keep the existing public signature."
```

One turn, one bill. The cost discipline of writing a complete brief is the same discipline that gets better code out — the two reinforce each other.

### Use the "ask tool" pattern in Agent mode [7]

When you're going to need iteration, instead of letting each clarification become a new turn, tell the agent up front to keep the loop *inside* the session:

> *"Use your ask tool to ask clarifying questions before writing code. When you have a plan, use the ask tool to confirm I'm happy with it. Iterate inside this session until I explicitly say I'm satisfied. Don't end the turn early."*

The agent now consolidates refinement into the same multi-step turn rather than spinning up new ones. Useful when you know the task will need 3–4 rounds of "no, more like this".

### Don't restart sessions you can keep

Counterpoint to "one task = one chat": within a single task, **don't restart unnecessarily**. Each restart loses the warm context cache (cached input is 10× cheaper than fresh input [2]), so the first turn of the new chat is the most expensive turn it'll have. If you're still on the same task, stay in the same chat.

The rule: **new chat per topic change, not per turn**.

---

## Lever 4 — Agent mode discipline

Agent mode is where the budget vanishes if you're casual. Treat it as a high-stakes mode, not a chat-with-tools.

### Front-load the brief

Open an agent session with everything the agent needs to know, in one prompt:

- **Purpose**: what's the actual goal in one sentence?
- **Scope**: which files / packages are in-scope? Which are out-of-scope?
- **Constraints**: what existing patterns must be preserved? What libraries are mandatory or forbidden?
- **Definition of Done**: how does the agent know to stop? (tests pass? specific file exists? feature works as described?)
- **Reporting**: at the end, summarize what changed and why.

Template:

> **Task**: Add a `/health` endpoint to the user-service that returns `{status: "ok", db: "ok"|"error"}`.
> **In scope**: `services/user/handlers/`, `services/user/tests/`.
> **Out of scope**: any other service, infra config, CI.
> **Constraints**: use the existing FastAPI patterns; do not add new dependencies.
> **Definition of Done**: endpoint responds correctly and a new test in `test_health.py` passes locally.
> **At the end**: list the files you touched and any assumptions you made.

A well-shaped brief routinely cuts agent sessions from 20 turns to 4–6.

### Pick the right model for the agent

The default "use Opus for everything in agent mode" instinct is expensive and often wrong:

- **Mechanical task** (rename, simple endpoint, scaffold tests): Haiku 4.5 or Gemini 3 Flash — saves 5–10× over premium.
- **Standard implementation** (multi-file refactor, new feature on known patterns): Sonnet 4.6 or GPT-5.4.
- **Genuinely hard reasoning** (tricky concurrency bug, performance investigation, architectural design): premium models earn their keep.

Use **Auto** model selection if you're uncertain — VS Code is supposed to route to a sensible default per turn. [10]

### Watch the token counter

The chat panel shows context-token usage in the bottom-right. Glance at it once or twice per agent session:

- Under ~30K tokens: comfortable.
- 30–80K: getting expensive, especially on premium models. Consider cutting losses if the agent is going in circles.
- 80K+: very expensive per turn. Better to stop, summarize, and start fresh than to keep paying full freight to re-read the entire session.

### Anti-pattern: re-running PR review on every push [6]

A Copilot PR review is one chat invocation against the entire diff. Re-running it after a one-line fix charges you for the whole diff again. Get one review, address it locally with smaller chat turns (or human review), and re-run Copilot only when the diff has *meaningfully* changed.

---

## Lever 5 — Surface choice

Always ask yourself: **am I using the right surface?**

| If you're trying to… | Use… | Don't use… |
|---|---|---|
| Finish a line / block of code | Inline completion (free) | Chat |
| Make the obvious next 3 mechanical edits | Next Edit Suggestions (free) | Edit mode |
| Understand what code does | Ask mode with `#selection` on a cheap model | Agent mode |
| Apply a focused diff across 2–3 files | Edit mode with explicit `#file:` targets | Agent mode |
| Implement a multi-step task autonomously | Agent mode with a front-loaded brief | Chat-and-paste loop |

The recurring mistake: reaching for the most powerful surface (Agent) and the most powerful model (Opus) reflexively. The right defaults are **cheaper surface + cheaper model + escalate when you actually need to**.

---

## Quick wins checklist

Adopt these immediately. They cost nothing and they all save credits.

- [ ] Set the default chat model to **Haiku 4.5** or **GPT-5 mini** in VS Code settings.
- [ ] Create `.github/copilot-instructions.md` in every active repo with your team conventions.
- [ ] Pin `04-cheatsheet.md` next to your monitor (or in your editor split).
- [ ] Bind a keyboard shortcut to **"New chat"** so starting fresh is one keystroke.
- [ ] Make a habit: glance at the **token counter** before sending a turn that already has >30K context.
- [ ] Stop using **drag-folder-into-chat** entirely. Always use `#file:` or `@workspace`.

---

## What you're trading

Some of these habits feel slower:

- Writing a complete prompt instead of chipping at it
- Front-loading an agent brief instead of "let's see what happens"
- Switching models mid-task instead of staying on Opus

The trade isn't latency vs. cost. It's **upfront thinking vs. downstream burn**. The optimizations above push the thinking to before the expensive call, which:

1. Saves credits — large effect
2. Improves output quality — usually meaningful effect
3. Costs a minute of upfront time — small effect

If a habit *doesn't* improve quality, it's still saving money. If it does both, it's a free upgrade.

---

## Sources

[2] GitHub Docs — *Models and pricing for GitHub Copilot* (cached-input pricing). <https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing>
[6] SmartScope — *GitHub Copilot Premium Request Optimization — Billing Mechanics and 8 Anti-Patterns.* <https://smartscope.blog/en/generative-ai/github-copilot/github-copilot-premium-request-optimization/>
[7] Alessio Franceschelli — *Stop wasting premium requests in GitHub Copilot: the ask tool trick.* <https://alessio.franceschelli.me/posts/ai/stop-wasting-premium-requests-in-github-copilot/>
[10] GitHub Community Discussion #163104 — *How to Optimise and Reduce Your Copilot Premium Request Usage.* <https://github.com/orgs/community/discussions/163104>

---

Next: [`04-cheatsheet.md`](04-cheatsheet.md) — the one-pager.
