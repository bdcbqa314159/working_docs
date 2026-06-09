# GitHub Copilot — Token & Cost Optimization

A teaching pack for the office on how to use **GitHub Copilot in VS Code** efficiently under the **new token-based billing** that went live on **1 June 2026**.

Goal: stop the new pricing from quietly draining the monthly AI Credit budget while preserving the productivity gains we already get from Copilot.

---

## Why this pack exists

On 1 June 2026 GitHub replaced the old **premium-request** system (each chat turn = 1 request, multiplied by a per-model factor) with a **token-based** system measured in **AI Credits** (1 credit = $0.01). Two consequences for us:

- The cost of a chat turn is no longer fixed; it depends on **how much context you attach** and **which model answers**.
- A single ill-shaped **agent session** can spend the entire monthly Pro allowance (\$10) in one go — real reports of \$30–\$40 burned in one sitting.

The two non-negotiable headlines:

1. **Code completions and Next Edit Suggestions are still free.** They do **not** consume AI Credits. Keep using them aggressively — they remain the cheapest, highest-leverage Copilot feature.
2. **Chat, Edit mode, Agent mode, and Code Review consume credits**, and the consumption is proportional to the **tokens** in (prompt + attached context + conversation history + tools' tool-call output) plus the **tokens** out (model's reply).

Everything in this pack flows from those two facts.

---

## Who this is for

Mixed audience: engineers who already use Copilot daily, plus those just starting. The pack is structured so each file can stand alone:

| File | Read it if you want… | Time |
|---|---|---|
| [`01-new-billing-model.md`](01-new-billing-model.md) | To understand what changed, the credit allowances, and the per-model price table | 10 min |
| [`02-vscode-surfaces.md`](02-vscode-surfaces.md) | To know what each VS Code Copilot surface (completion, chat, edit, agent) costs | 10 min |
| [`03-optimization-playbook.md`](03-optimization-playbook.md) | Practical anti-patterns + tactics to halve your credit burn | 25 min |
| [`04-cheatsheet.md`](04-cheatsheet.md) | A one-page reference to print and pin next to the monitor | 2 min |
| [`05-presentation.md`](05-presentation.md) | Marp-compatible slide deck for a 20-minute office talk | — |
| [`appendix-sources.md`](appendix-sources.md) | Where every number in this pack came from, with links | — |

## How to use this pack

- **Self-teach**: read `01` → `02` → `03` in order. Pin `04` somewhere visible.
- **Teach the team**: open `05-presentation.md` in Marp (VS Code extension *Marp for VS Code*) and present, or export to PDF (`Marp: Export slide deck...` → PDF).
- **Highlight & share**: markdown renders with highlight support in GitHub, GitLab, Obsidian, Notion, and most internal wikis. Drop these files into your team's space as-is.

## What this pack is NOT

- Not legal/contract advice — confirm seat counts and credit pools with whoever holds the GitHub enterprise contract.
- Not a hard guarantee of prices — model rates change. The structure of the system is stable; specific numbers in `01-new-billing-model.md` reflect the GitHub docs as of **June 2026**.
- Not a Copilot alternatives comparison. Scope here is: **make our existing seats go further**.

---

*Last verified: 2026-06-08 against `docs.github.com/en/copilot/reference/copilot-billing/`.*
