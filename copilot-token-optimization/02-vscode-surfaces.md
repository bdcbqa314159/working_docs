# 2. The VS Code Copilot surfaces — and what each one costs

The Copilot plugin in VS Code is not one feature; it's **five distinct surfaces**, each with very different cost behaviour. Knowing which surface you're using is the single biggest determinant of how fast your credits drain.

## The cost map at a glance

| Surface | How you trigger it | Bills credits? | Typical tokens per turn | Cost shape |
|---|---|---|---|---|
| **Code completion** | Just type — ghost text appears | **No** | n/a | Free, unlimited |
| **Next Edit Suggestions** (NES) | Tab through proposed next edits | **No** | n/a | Free, unlimited |
| **Chat — Ask mode** | Side panel, "@workspace" or plain question | **Yes** | ~3–15K in, ~0.5–2K out | Small per turn, but easy to multiply |
| **Chat — Edit mode** | Side panel, "Edits" target with selected files | **Yes** | ~10–40K in, ~1–4K out | Medium per turn; cost ∝ files edited |
| **Chat — Agent mode** | Side panel, "Agent" mode + tools enabled | **Yes** | 50K–500K cumulative | **Highest** — loops + tool output re-injection |
| **Code Review** (PR or inline) | "Copilot review" on a PR or selection | **Yes** | depends on diff size | Per review, on top of any chat use |

Read the rest of this file as: **what's actually going into the token count on each paid surface**, and how to keep it small.

---

## Surface A — Code completion (the free one)

The classic ghost-text suggestion as you type. **Does not bill against AI Credits.** [1] [2] Internally it runs on a fast, smaller model that GitHub absorbs the cost of.

Implications:

- Use it as much as you want. There is no per-completion meter.
- It is **not the right surface** when you need conversation, planning, or multi-file refactoring — for those, switch to chat. But if your task is "complete this line / this block", do **not** open chat. Inline completion is the right tool and it's free.
- Toggle it off when you don't want it (`Ctrl+Shift+P` → `Copilot: Disable Completions in <language>`). Off ≠ free savings (it was already free), but turning off completions for languages where it pollutes more than it helps reduces noise and tab-acceptance mistakes.

## Surface B — Next Edit Suggestions (also free)

NES proposes the **next change you're likely to make** based on the change you just made. Tab to accept the next jump+edit, or `Esc` to dismiss.

Implications:

- Also free. [1] [2] Same reasoning as completions.
- High leverage on **mechanical edits**: rename propagation, adding a parameter that needs threading through callers, mirroring a pattern across a few files.
- The right surface for "I just did X; now do the obvious Y" loops. Reaching for chat to do these is a categorical waste of credits.

## Surface C — Chat, Ask mode (paid)

Open the Copilot side panel, leave the mode set to "Ask". This is conversational Q&A — you ask, it answers, no file edits applied automatically.

**What goes into the input tokens:**

1. Your prompt text
2. Any context you attached (`#file:foo.py`, `#selection`, `#editor`, `#codebase`, dragged files)
3. The **entire conversation history of the current chat** (every turn you've had, both sides)
4. The system prompt + tools list (GitHub-managed; you can't shrink it directly)

**Important — what is NOT automatically attached**: the file you have open in the editor is *not* sent unless you reference it with `#editor`, `#file:<name>`, or use `@workspace`. (`@workspace` *does* pull in workspace context — see below.) Many users assume Copilot already knows the open file. Sometimes it does, sometimes it doesn't, depending on chat-variable defaults. **When in doubt, explicitly attach with `#file`** — both for correctness *and* so you can see what's being charged for.

**Context variables — token cost ranking from cheapest to most expensive:** [9]

| Variable | What it attaches | Approx. token cost |
|---|---|---|
| `#selection` | Just your highlighted code | Tiny (10s–100s of tokens) |
| `#editor` | The currently focused editor's file | Small–medium (size of one file) |
| `#file:<name>` | A specific file you name | Small–medium |
| `@workspace` / `#codebase` | A **retrieved** subset of repo files relevant to your prompt | Medium–large (multi-file, retrieved) |
| Dragging a folder in | Every file under it | **Huge** — careful |

**Tip**: `@workspace` (now also exposed as `#codebase`) does *retrieval* rather than dumping the whole repo — it picks files it thinks are relevant. That's better than dragging in folders, but it's still bigger than `#file:` and you have less control over what was selected.

**Output tokens** in Ask mode are usually modest — you're getting back an explanation, a code snippet, or a plan, not a full file. The dominant cost is **input**, especially if your conversation has been running for a while and the history is large.

## Surface D — Chat, Edit mode (paid, more expensive than Ask)

Switch the side-panel mode to "Edits". You designate files as the **edit target**, give an instruction, and Copilot proposes a multi-file diff that you accept or reject.

**Why it's more expensive than Ask:**

- The model needs the **full content of every target file** in input — not a snippet, not retrieval, the whole file. Bigger files → linearly more input cost.
- It typically generates a **whole-file rewrite** in output for each touched file. Output tokens are much pricier than input tokens (Sonnet: \$15 vs \$3 per million). A 500-line file regenerated is several thousand output tokens at \$15/M.
- If your prompt is vague, the model may rewrite more than you intended — generating more output tokens than necessary.

**Practical guidance:**

- Don't target a 2000-line file when you mean to change 30 lines. Either select the range first, or copy the function to a smaller scratch file.
- Be **specific** about what to change ("rename `getUserData` to `fetchUserProfile` and update all callers within these two files"), not aspirational ("make this cleaner"). Specific instructions → smaller, focused diffs → fewer output tokens.
- Prefer Ask mode (then apply the patch manually) when the change is small or you want to review the reasoning before code is touched.

## Surface E — Chat, Agent mode (paid, **most expensive**)

Agent mode in VS Code lets the model **call tools** — read files, run commands, edit files, run tests — in a loop until it decides it's done. This is the "Copilot does the whole task" mode.

**Why it dominates the credit bill:**

Each loop iteration costs you the input it sees that turn, which includes:

- The original prompt
- All prior turns in this agent session
- **Every tool's output from every prior turn** (file contents read, command outputs, test results)

That last point is the cost killer. Read a 1000-line file at turn 2 → those 1000 lines are in every subsequent turn's input until the agent decides to "forget" them. Agent sessions routinely accumulate **hundreds of thousands of input tokens** over 10–20 tool calls.

The realistic per-session range is **\$0.50 to \$5+** on a premium model — and reports of \$30–40 sessions exist for very long Opus-driven runs that recursed through tests and fixes. [5] [8]

**Practical guidance — see `03-optimization-playbook.md` section "Agent mode discipline" for the full set.** The headline rules:

1. **One task, one session** — don't reuse a 30-turn agent context for an unrelated new task.
2. **Front-load the brief** — purpose, constraints, definition of done, things to NOT touch — so the agent doesn't burn turns asking clarifying questions.
3. **Pick a smaller model for agent loops** when the task is mechanical. Haiku 4.5 at \$1/M input is **5× cheaper than Opus** and often enough.
4. **Watch the token counter** in the bottom-right of the chat panel. If it's climbing past 50K mid-session, consider cutting losses and starting fresh.

## Surface F — Code review (paid, lumpy)

Triggering Copilot to review a PR or a code selection costs credits **per review**, with cost proportional to the size of the diff being reviewed plus the model's output (the comments it writes).

- Cheap on small diffs (~20–50 lines): a few cents.
- Expensive on large diffs (500+ lines): can hit several dollars on a premium model.
- **Don't re-trigger a Copilot review for every minor amendment.** Push, get one review, address it locally, and run Copilot again only when the diff has meaningfully changed. Use human review for the small follow-ups.

---

## Mental model: where the tokens come from

A useful way to picture cost on any paid surface:

```
cost = (your prompt + attached context + chat history + tool output history) × input_rate
     + (model's reply + new tool call arguments) × output_rate
```

You control four levers, in roughly this order of impact:

1. **Which model** — picks the rate (10× spread between cheapest and most expensive).
2. **Tool output history** — agent-mode-only, but dominates totals there. Shorter sessions = less re-injected output.
3. **Attached context size** — `#selection` vs `@workspace` vs dragged folder.
4. **Chat history length** — start a new chat when you change topic.

The next file is the practical playbook for each of those levers.

---

## Sources

[1] GitHub Blog — *GitHub Copilot is moving to usage-based billing.* <https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/>
[2] GitHub Docs — *Models and pricing for GitHub Copilot.* <https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing>
[5] TechJournal — *GitHub Copilot Token Billing Starts Today: Devs Report 10x-50x Cost Increases.* <https://techjournal.org/github-copilot-token-billing-backlash>
[8] ChatForest — *GitHub Copilot's Token Billing Is Live.* <https://chatforest.com/builders-log/github-copilot-token-billing-agentic-cost-builder-guide/>
[9] VS Code Docs — *GitHub Copilot frequently asked questions.* <https://code.visualstudio.com/docs/copilot/faq>

---

Next: [`03-optimization-playbook.md`](03-optimization-playbook.md) — the practical playbook.
