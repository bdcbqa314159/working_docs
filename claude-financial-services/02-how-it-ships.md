# 2. How Claude for Financial Services ships — subscriptions, deployment, what unlocks what

To use any of this in the office we'd need one of the access paths below. This file is the map of which path provides which capability, with current 2026 pricing where Anthropic publishes it.

## The three access paths

There are essentially three ways an organisation gets Claude for Financial Services capabilities:

### Path A — Claude for Microsoft 365 + Claude Cowork plugins

The "polished, in-the-flow-of-work" path.

- **What it gives you**: Claude appearing as a panel inside Excel, PowerPoint, Word, Outlook. The 10 FS agents available as installable plugins. Claude Cowork as the orchestration surface. [1] [2]
- **Requires**: a Claude Team or Enterprise subscription, plus the Claude for Microsoft 365 admin install on the tenant. [5] [7] [8]
- **Pricing reference**:
  - Claude Team: **\$20 / seat / month**, minimum 5 seats (Standard). Claude Code is a separate Premium seat at \$100 / seat / month. [8]
  - Claude Enterprise: published base **~\$20 / user / month**, but in 2026 the base seat fee no longer bundles AI usage — **token usage is billed separately at API rates** on top of the seat fee. Realistic all-in cost for moderately heavy users: **\$60–\$250+ / user / month**. [7] [9]
- **Plugins required**: the FS plugins listed in section 1 are installed at the workspace level by an admin. [5]
- **BYOC routing option (material for a regulated firm)**: the M365 add-in can be deployed against your firm's **own cloud** — Google Vertex AI, AWS Bedrock, or an internal LLM gateway — instead of routing traffic to Anthropic's API. The repo ships a Claude Code plugin called `claude-for-msft-365-install` that walks an IT admin through generating the customised add-in manifest, granting Azure admin consent, and writing per-user routing config via Microsoft Graph. End-user experience is identical; the data path becomes Excel → your cloud → Claude on your cloud → back. Compliance posture is then whatever you already have for that cloud (DPAs, retention, egress controls). [4]

### Path B — Claude Code plugins (developer-facing)

For workflows where the FS agents are invoked from a terminal or scripted from inside engineering work.

- **What it gives you**: the agent templates as `claude plugin install ...` packages, runnable from Claude Code. [4]
- **Requires**: Claude Code access — bundled with paid plans (Pro, Pro+, Team Premium seat at \$100 / seat / month, Enterprise). [8]
- **Limitation in our context**: Claude Code is a developer tool. It works for the *coded* parts of FS workflows (build a data pipeline, generate a report) but is not the right surface for an analyst working in PowerPoint.

### Path C — Claude Managed Agents (API-driven)

The platform path: agents run as services behind a firm's own workflow engine.

- **What it gives you**: the agent templates as deployable cookbooks, callable via the Anthropic API. [1] [4]
- **Requires**: organisational Anthropic API access; engineering work to deploy the cookbooks; data connectors set up against firm systems.
- **Cost model**: pure consumption — pay per token at the published per-model rates (Opus 4.7 ≈ \$5/M input + \$25/M output, etc., same rate card as the [Copilot pack](../copilot-token-optimization/01-new-billing-model.md) references). No seat fee.
- **In practice**: this is how a platform team integrates Claude into existing workflow infrastructure. It's the most flexible path and the one most regulated firms end up choosing once they're serious — but it's also the one with the most engineering work upfront.

## The open-source angle (important nuance) [4]

The 10 agent templates, plus 40+ skills and slash commands, plus 11 MCP connectors, are published in **[github.com/anthropics/financial-services](https://github.com/anthropics/financial-services)** under the **Apache License 2.0**.

What this means concretely:

- The templates themselves are **inspectable, forkable, modifiable**. The "skills" are markdown files; the "agents" are YAML configurations; the connectors are MCP server definitions. None of this is proprietary IP behind a license wall.
- Running them **still requires Claude API or subscription access** — the templates orchestrate Claude calls, they aren't standalone models.
- This is unusual for an enterprise-aimed vertical product. It says Anthropic is betting on the model + governance layer as the moat, and treating the workflow library as a giveaway to accelerate adoption.

For us: the open-source repo is a reasonable *educational* resource even without subscription access. We can read the markdown skill files to understand what "a senior banker doing this task" looks like as written-down instructions. We can read the cookbooks to understand the integration patterns. **What we cannot do** is run them — that requires either a subscription (paths A or B) or org-level API access (path C).

## Required-for-FS-deployment controls

These are the controls a regulated firm typically needs before deploying *any* AI tool, not just Claude. Listed because they're the practical gate for getting any of paths A/B/C past compliance:

- SSO with the firm's identity provider
- Custom data retention (often "zero retention" of inputs/outputs by Anthropic)
- Audit logging into the firm's SIEM
- Per-user / per-team usage controls and quotas
- Data residency commitments (EU vs US, etc.)
- Vendor risk assessment + DPA + appropriate certifications

Anthropic publishes ISO/IEC 42001:2023 certification and supports the controls above on the Enterprise tier. Whether our compliance team would sign off is a separate conversation.

## What "M365 Copilot" gives us today, for comparison

So the gap is visible:

| Capability | M365 Copilot (we have) | Claude for FS (we don't) |
|---|---|---|
| Drafting in Word / Excel / PowerPoint / Outlook | Yes | Yes |
| Reading Outlook / SharePoint / Teams for context | Yes (native) | No (no equivalent connector) |
| Connectors to FactSet / S&P / PitchBook / Moody's / etc. | No (generic web) | Yes (governed MCP) |
| Pre-built financial agent templates | Limited (Financial Reconciliation Agent for Dynamics 365, Variance Analysis Agent) | Yes (10 templates) |
| Complex Excel reasoning (FMW-style tasks) | Reasonable | Best-in-class (Opus 4.7) |
| Long-context document analysis | Modest (~64K useful in practice) | 500K input context |
| Source attribution on every output | Limited | Yes, by design |
| Runs autonomously (Managed Agents) | Limited (Copilot Studio agents) | Yes (managed agents API) |

This isn't "M365 Copilot is bad". [12] [13] M365 Copilot is genuinely strong where the work lives inside Microsoft's surfaces — that includes a lot of what analysts do. But the FS-specific agentic layer is currently only on Claude's side.

---

## Sources

[1] Anthropic — *Agents for financial services.* <https://www.anthropic.com/news/finance-agents>
[2] Anthropic — *Claude for Financial Services solutions page.* <https://claude.com/solutions/financial-services>
[4] GitHub — *anthropics/financial-services repository* (Apache 2.0). <https://github.com/anthropics/financial-services>
[5] Claude Help Center — *Install financial services plugins.* <https://support.claude.com/en/articles/13851150-install-financial-services-plugins>
[7] Claude Help Center — *What is the Enterprise plan?* <https://support.claude.com/en/articles/9797531-what-is-the-enterprise-plan>
[8] Claude Help Center — *What is the Team plan?* <https://support.claude.com/en/articles/9266767-what-is-the-team-plan>
[9] Runbear — *Claude Enterprise pricing in 2026: what mid-market teams actually pay.* <https://runbear.io/posts/claude-enterprise-pricing-mid-market>
[12] Microsoft — *Compare Copilot vs. Claude Enterprise.* <https://www.microsoft.com/en-us/microsoft-365-copilot/copilot-vs-claude-enterprise>
[13] Ninetwothree — *Claude vs. Microsoft Copilot for Excel: Which One for Your Work?* <https://www.ninetwothree.co/blog/claude-vs-microsoft-copilot-for-excel>

---

Next: [`03-our-access-situation.md`](03-our-access-situation.md) — the honest articulation of where we stand.
