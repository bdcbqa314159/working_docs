# 1. The new billing model — what actually changed

## TL;DR

- **Old (pre 1 June 2026)**: each chat/agent turn = **1 "premium request"**, multiplied by a fixed per-model factor (Sonnet 1×, Opus 10× or 30×, GPT-4o 0×, etc.). Plans gave you a fixed monthly *count* of premium requests. [4]
- **New (from 1 June 2026)**: you no longer have a request count. You have a monthly **AI Credit budget in dollars**, and every paid surface bills against it **by tokens consumed × the per-model rate**. [1]

| What | Old system | New system |
|---|---|---|
| Unit | "Premium request" | AI Credit (`1 credit = $0.01`) [2] |
| What you spend | Counts of requests | Tokens × per-model price |
| Plan allowance | N requests / month | \$ in credits / month |
| Surfaces affected | Chat, edits, agent | **Same** — chat, edits, agent, code review |
| Still free | Code completion, Next Edit | Code completion, Next Edit |
| Annual subscribers | — | Stay on legacy multipliers until renewal, then move over |

The legacy system isn't gone — annual Pro/Pro+ subscribers stay on premium requests with revised multipliers until their term expires. [4] For most office monthly seats: **you are on the new token system as of 1 June 2026**. [1]

## Monthly credit allowance per plan [1] [3]

| Plan | Monthly price | Monthly AI Credits |
|---|---|---|
| Copilot Pro (individual) | \$10 | \$10 |
| Copilot Pro+ (individual) | \$39 | \$39 |
| Copilot Business (per seat) | \$19 | \$19 |
| Copilot Enterprise (per seat) | \$39 | \$39 |

Two things to keep in mind:

1. The credit pool is **per user, per month, no rollover**. Unused credits at month-end are gone.
2. Overage is **purchasable** on paid plans — i.e. once the included pool is empty, your seat keeps working but additional tokens bill out-of-pocket (subject to admin policy in your org). Confirm with your admin whether overage spending is enabled or capped.

## Token pricing — the rate card [2]

All prices below are taken from the GitHub Copilot models-and-pricing reference page as of June 2026. Prices are **per 1 million tokens**, denominated in USD (i.e. in AI Credits at 100 credits = \$1).

Every model has three numbers that matter:

- **Input** — text you send: prompt + chat history + attached files + tool output that comes back into the model
- **Cached input** — repeat input that was seen recently (file you re-attach, conversation tail). Cached tokens are **10× cheaper** than fresh input on every model below.
- **Output** — what the model writes back

### OpenAI

| Model | Input | Cached input | Output |
|---|---|---|---|
| GPT-5 mini | \$0.25 | \$0.025 | \$2.00 |
| GPT-5.3-Codex | \$1.75 | \$0.175 | \$14.00 |
| GPT-5.4 (≤272K context) | \$2.50 | \$0.25 | \$15.00 |
| GPT-5.4 (>272K context) | \$5.00 | \$0.50 | \$22.50 |
| GPT-5.4 mini | \$0.75 | \$0.075 | \$4.50 |
| GPT-5.4 nano | \$0.20 | \$0.02 | \$1.25 |
| GPT-5.5 (≤272K context) | \$5.00 | \$0.50 | \$30.00 |
| GPT-5.5 (>272K context) | \$10.00 | \$1.00 | \$45.00 |

### Anthropic

| Model | Input | Cached input | Cache write | Output |
|---|---|---|---|---|
| Claude Haiku 4.5 | \$1.00 | \$0.10 | \$1.25 | \$5.00 |
| Claude Sonnet 4 / 4.5 / 4.6 | \$3.00 | \$0.30 | \$3.75 | \$15.00 |
| Claude Opus 4.5 / 4.6 / 4.7 / 4.8 | \$5.00 | \$0.50 | \$6.25 | \$25.00 |

### Google

| Model | Input | Cached input | Output |
|---|---|---|---|
| Gemini 2.5 Pro | \$1.25 | \$0.125 | \$10.00 |
| Gemini 3 Flash | \$0.50 | \$0.05 | \$3.00 |
| Gemini 3.1 Pro (≤200K context) | \$2.00 | \$0.20 | \$12.00 |
| Gemini 3.1 Pro (>200K context) | \$4.00 | \$0.40 | \$18.00 |
| Gemini 3.5 Flash | \$1.50 | \$0.15 | \$9.00 |

### Other

| Model | Input | Cached input | Output |
|---|---|---|---|
| Raptor mini | \$0.25 | \$0.025 | \$2.00 |
| MAI-Code-1-Flash | \$0.75 | \$0.075 | \$4.50 |

## What these numbers mean in practice

Three back-of-envelope conversions to internalize:

**Conversion 1 — Sonnet 4.6 on a normal chat turn**: ~5K tokens of context in, ~1K tokens out. Cost: `5K × $3 + 1K × $15 = $0.015 + $0.015 = $0.030 = 3 credits`. So Pro's \$10 allowance buys roughly **330 such turns/month** on Sonnet 4.6.

**Conversion 2 — Opus on a heavy refactor turn**: ~30K tokens in (your file + 3 imports + the history), ~3K tokens out. Cost: `30K × $5 + 3K × $25 = $0.150 + $0.075 = $0.225 = 22.5 credits`. Pro's \$10 buys roughly **44 such turns**.

**Conversion 3 — Agent session with 20 tool calls on Opus**: ~200K tokens cumulative in (each tool result re-enters context), ~15K tokens out. Cost: `200K × $5 + 15K × $25 = $1.00 + $0.375 = $1.375 = 137.5 credits`. **One agent session ≈ 14% of Pro's monthly pool.**

This is the math behind the public reports of devs blowing through \$10 in a single morning. [5] [8] The pricing isn't punitive per turn — it's that **agents loop**, and each loop's tool output gets re-injected into every subsequent turn.

## The free lane — keep using it

Two surfaces remain unmetered: [1] [2]

- **Code completion** (ghost-text in the editor as you type)
- **Next Edit Suggestions** (the multi-line "predict my next change" overlay)

These are the highest-frequency Copilot interactions for most of us — typically hundreds of completions per workday — and **none of them cost a credit**. The bulk of Copilot's productivity benefit comes from this lane. Optimization advice in this pack is about preserving that benefit while spending dramatically less on the chat/agent lane.

---

## Sources

[1] GitHub Blog — *GitHub Copilot is moving to usage-based billing.* <https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/>
[2] GitHub Docs — *Models and pricing for GitHub Copilot.* <https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing>
[3] GitHub Docs — *Plans for GitHub Copilot.* <https://docs.github.com/en/copilot/get-started/plans>
[4] GitHub Docs — *Model multipliers for annual plans on request-based billing (legacy).* <https://docs.github.com/en/copilot/reference/copilot-billing/model-multipliers-for-annual-plans>
[5] TechJournal — *GitHub Copilot Token Billing Starts Today: Devs Report 10x-50x Cost Increases.* <https://techjournal.org/github-copilot-token-billing-backlash>
[8] ChatForest — *GitHub Copilot's Token Billing Is Live.* <https://chatforest.com/builders-log/github-copilot-token-billing-agentic-cost-builder-guide/>

---

Next: [`02-vscode-surfaces.md`](02-vscode-surfaces.md) — what each VS Code surface costs in practice.
