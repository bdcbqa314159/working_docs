# Copilot in VS Code — One-Page Cheat Sheet

*New token-based billing, effective 1 June 2026. 1 AI Credit = \$0.01.*

---

## Free, unlimited — use freely

- **Inline code completion** (ghost text as you type)
- **Next Edit Suggestions** (Tab through proposed next changes)

## Paid — cost ∝ tokens × model rate

- **Chat — Ask mode** (small per turn)
- **Chat — Edit mode** (medium — whole file in & out)
- **Chat — Agent mode** (**largest** — every tool output re-injected)
- **Copilot code review** (per review, cost ∝ diff size)

---

## The cost levers, in priority order

1. **Model**: Haiku 4.5 / GPT-5 mini / Gemini 3 Flash ≈ **5–10× cheaper** than Opus / GPT-5.5. Default to a cheap one.
2. **Agent session length**: tool output stacks. New chat per topic.
3. **Context size**: `#selection` ≪ `#editor` ≪ `#file:` ≪ `@workspace` ≪ dragged folder.
4. **Chat history**: long chats = expensive turns. New chat per topic change.

---

## The two-lane workflow

```
                  ┌────────────────────────────┐
   EXPLORE  →     │ Cheap lane (Haiku, mini)   │   ← ask, plan, summarise
                  └────────────┬───────────────┘
                               │ plan locked
                               ▼
                  ┌────────────────────────────┐
   EXECUTE  →     │ Premium lane (Sonnet+)     │   ← one well-formed implementation turn
                  └────────────┬───────────────┘
                               │
                               ▼
                  ┌────────────────────────────┐
   VERIFY   →     │ Cheap lane again           │   ← review the diff, write tests
                  └────────────────────────────┘
```

---

## Per-surface guidance

| Doing… | Use | Avoid |
|---|---|---|
| Completing code in place | Inline completion **(free)** | Chat |
| Mechanical next-3-edits | Next Edit Suggestions **(free)** | Edit mode |
| "What does this do?" | Ask mode, cheap model, `#selection` | Agent mode |
| 2–3 file focused diff | Edit mode, `#file:` targets | Agent mode |
| Multi-step autonomous task | Agent mode + front-loaded brief | Casual chat with tools |

---

## Stop doing this

- ❌ Asking yes/no on Opus
- ❌ Dragging folders into chat
- ❌ "Refactor this" → "actually..." → "now do..." (prompt-chipping)
- ❌ Re-running PR review after every push
- ❌ Reusing a 30-turn agent session for a new task
- ❌ Defaulting to Agent mode for things Ask could do

## Start doing this

- ✅ Set default model to a cheap one (Haiku 4.5 / GPT-5 mini)
- ✅ One complete prompt instead of four chipped ones
- ✅ `#file:` over `@workspace` over dragging
- ✅ `.github/copilot-instructions.md` for repo conventions
- ✅ `+ New Chat` every time you change topic
- ✅ Glance at the token counter (bottom-right of chat) before sending a big turn

---

## Agent-mode brief template

```
Task: <one sentence>.
In scope: <files / packages>.
Out of scope: <what NOT to touch>.
Constraints: <patterns to preserve, libs required/forbidden>.
Definition of Done: <how the agent knows to stop>.
At the end: <summarise files touched + assumptions>.
```

---

## Order-of-magnitude pricing (per 1M tokens, USD)

| Tier | Example | Input | Output |
|---|---|---|---|
| Cheap | Haiku 4.5 | \$1.00 | \$5.00 |
| Cheap | GPT-5 mini | \$0.25 | \$2.00 |
| Cheap | Gemini 3 Flash | \$0.50 | \$3.00 |
| Standard | Sonnet 4.6 | \$3.00 | \$15.00 |
| Standard | GPT-5.4 | \$2.50 | \$15.00 |
| Premium | Opus 4.7 | \$5.00 | \$25.00 |
| Premium | GPT-5.5 | \$5.00 | \$30.00 |

**Cached input is 10× cheaper** on every model. Re-attaching the same file within a few minutes is much cheaper than the first time.

---

## Monthly allowance reminder

| Plan | Credits / month |
|---|---|
| Pro | \$10 |
| Pro+ | \$39 |
| Business | \$19 / seat |
| Enterprise | \$39 / seat |

*No rollover. Overage is per-token at the rates above (subject to admin policy).*

---

*Verified June 2026. Numbers move — check `docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing` if you're making procurement decisions.*
