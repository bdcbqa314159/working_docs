# 3. Our access situation — the direct version

This file exists to settle the question cleanly so the team isn't operating on rumour.

## What we have

| Tool | What it is | What it covers |
|---|---|---|
| **Microsoft 365 Copilot** | The Microsoft-bundled AI layer across Word, Excel, PowerPoint, Outlook, Teams, SharePoint | Drafting, summarising, in-app assistance across M365 |
| **GitHub Copilot** | The code-completion + chat + agent tool inside VS Code (and other IDEs) | Code generation, code review, multi-file edits in the editor |

That's it on the AI-tooling side. There is no sanctioned org-level access to:

- **Claude.ai** (the consumer app)
- **Claude Team or Enterprise** (the subscription that unlocks Cowork, the M365 plugin, and the FS agents)
- **Claude for Microsoft 365** (the Excel/PPT/Word/Outlook plugin)
- **Claude Cowork** (the orchestration surface for the FS agents)
- **Claude Code** (the developer CLI)
- **Anthropic API** at the org level (for Managed Agents)

## What this means for Claude for Financial Services

The 10 FS agent templates, the M365 plugin, the data connectors — **all of it requires a Claude subscription or Anthropic API access we don't have**. [5] [7] [8] There is no path to using them through M365 Copilot or GitHub Copilot. The two product families are separate; one isn't a backdoor to the other.

This is true even though some of us hold **personal** Claude subscriptions. A personal account is not a sanctioned channel for office work:

- Personal accounts have no DPA with our firm.
- They have no audit logging routed into our compliance posture.
- They have default Anthropic data retention (not the "zero retention" enterprise configuration).
- Using a personal account on office data would be a data-handling issue *regardless* of how useful the output looks.

So the rule is simple: **personal Claude is for personal exploration; office work goes through office-sanctioned tools**.

## Why this is the situation (not a complaint, just the facts)

There's no story to read into the access landscape. It is what it is:

- M365 Copilot came in via the Microsoft enterprise agreement. It was a natural addition; the firm already runs on M365.
- GitHub Copilot came in via the GitHub enterprise agreement. Same logic.
- Claude has not been added via an Anthropic agreement. That would be a separate procurement track, with separate vendor risk assessment, separate DPA, separate budget.

Adding Claude is not impossible — it's a procurement decision. But it isn't decided, and we shouldn't assume it.

## What we are NOT saying

To pre-empt the four most likely misreadings:

1. **We are not saying M365 Copilot is bad.** It's actually well-suited to a lot of FS-flavoured work that happens inside Microsoft surfaces — see `04-what-we-can-do-today.md`.
2. **We are not saying Claude is necessarily better.** On *complex spreadsheet reasoning and long-context analysis*, the public benchmarks favour Claude. [1] [13] On *workflows that live inside M365's connected apps*, Copilot's tight integration is a real advantage. [12] They aren't the same tool.
3. **We are not lobbying for procurement.** This pack is informational. If anyone wants to build a business case for adding Claude, that's a separate document with cost models and use-case prioritisation.
4. **We are not encouraging personal-account workarounds for office work.** The opposite — see the boundary in `04`.

## What we ARE saying

Three things:

1. **The Claude for Financial Services offering is real, well-engineered, and relevant to our discipline.** People asking about it are asking a sensible question.
2. **We do not have access to it today through any of the office's current AI subscriptions.** This won't change without a procurement decision.
3. **We can still get value from understanding what it is** — both to make informed judgements about future tooling decisions, and to recognise which workflows it would meaningfully change for us if and when access ever arrives.

## What to tell colleagues asking about it

A clean two-sentence version:

> *Yes — Anthropic launched Claude for Financial Services in May. It's a strong product for our type of work, but we don't have a sanctioned channel to use it: our office AI tooling today is Microsoft 365 Copilot and GitHub Copilot, and Claude requires a separate subscription we haven't acquired.*

If they push further on "can I just use my personal Claude account?":

> *Not on office data, no — that would be a data-handling issue regardless of how useful the output is. Personal accounts have no DPA, no audit routing, and default retention settings. Personal Claude is fine for personal exploration; office work goes through office-sanctioned tools.*

---

## Sources

[1] Anthropic — *Agents for financial services* (Opus 4.7 benchmark claims). <https://www.anthropic.com/news/finance-agents>
[5] Claude Help Center — *Install financial services plugins.* <https://support.claude.com/en/articles/13851150-install-financial-services-plugins>
[7] Claude Help Center — *What is the Enterprise plan?* <https://support.claude.com/en/articles/9797531-what-is-the-enterprise-plan>
[8] Claude Help Center — *What is the Team plan?* <https://support.claude.com/en/articles/9266767-what-is-the-team-plan>
[12] Microsoft — *Compare Copilot vs. Claude Enterprise.* <https://www.microsoft.com/en-us/microsoft-365-copilot/copilot-vs-claude-enterprise>
[13] Ninetwothree — *Claude vs. Microsoft Copilot for Excel.* <https://www.ninetwothree.co/blog/claude-vs-microsoft-copilot-for-excel>

---

Next: [`04-what-we-can-do-today.md`](04-what-we-can-do-today.md) — pragmatic guidance with the tools we have.
