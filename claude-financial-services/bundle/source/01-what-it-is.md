# 1. What Claude for Financial Services actually is

A factual overview of what Anthropic announced and shipped, as of June 2026.

## The announcement in one paragraph

On **5 May 2026**, Anthropic launched **Claude for Financial Services**: a vertically-focused product line consisting of (a) **10 ready-to-run agent templates** for high-volume FS workflows, (b) **deep integration with Microsoft 365 apps** (Excel, PowerPoint, Word, Outlook), (c) **MCP-based data connectors** to ~11 financial data providers, and (d) **enterprise controls** (SSO, SCIM, audit logs, custom retention, ISO/IEC 42001:2023 certification). [1] [2] The underlying model — **Claude Opus 4.7** — leads industry benchmarks on financial tasks (Vals AI Finance Agent: 64.37%). [1]

The whole release is a coordinated bet that financial-services workflows are different enough from generic enterprise productivity to warrant a dedicated product surface.

---

## The 10 agent templates [1]

Organized into two groups of five.

### Research & Client Coverage

| # | Agent | What it does | Typical output |
|---|---|---|---|
| 1 | **Pitch Builder** | Creates target lists, runs comparables, drafts pitchbooks | Comps model (Excel), pitchbook (PowerPoint), cover note (Outlook) |
| 2 | **Meeting Preparer** | Assembles client and counterparty briefs ahead of calls | Pre-call briefing document |
| 3 | **Earnings Reviewer** | Reads transcripts and filings, updates models, flags thesis-relevant changes | Updated model + flagged-changes summary |
| 4 | **Model Builder** | Builds and maintains financial models from filings, data feeds, analyst inputs | Live financial model with refresh logic |
| 5 | **Market Researcher** | Tracks sector and issuer developments, synthesises news, filings, broker research | Synthesised intel pack with items flagged for review |

### Finance & Operations

| # | Agent | What it does | Typical output |
|---|---|---|---|
| 6 | **Valuation Reviewer** | Checks valuations against comparables, methodology, firm standards | Validation report + methodology assessment |
| 7 | **General Ledger Reconciler** | Reconciles GL accounts, runs NAV calculations | Reconciliation + NAV report |
| 8 | **Month-End Closer** | Runs close checklist, prepares journal entries, produces close reports | Journal entries + close report |
| 9 | **Statement Auditor** | Reviews financial statements for consistency, completeness, audit-readiness | Audit-ready statements with flags |
| 10 | **KYC Screener** | Assembles entity files, reviews source documents, packages escalations | KYC file with compliance escalations |

## How each template is built [1] [4]

Each agent template is not a single prompt; it is a **bundle of three things**:

- **Skills** — markdown-defined instructions and domain knowledge for the task (think: "how a senior banker would do this", written down).
- **Connectors** — governed access to the data the task runs on. MCP-based, so the data fetch is auditable and scoped.
- **Subagents** — additional Claude models the main agent calls for specific sub-tasks (e.g. a comparables-selection subagent, a methodology-check subagent, a sensitivity-runner subagent).

This three-layer structure is the design innovation. It means the templates are not black boxes: skills are inspectable markdown, connectors have explicit scopes, and subagents are addressable individually.

## Microsoft 365 integration [1] [2]

This is the part that overlaps most with our existing M365 Copilot — and where the comparison is sharpest. Claude's M365 plugin:

- **Excel** — builds financial models from filings and data feeds; audits formulas across linked workbooks; runs sensitivity analyses.
- **PowerPoint** — drafts decks that auto-update when underlying numbers change.
- **Word** — edits credit memos (and similar long-form docs) against a firm's own templates.
- **Outlook** — drafts cover notes for pitchbooks and similar outbound communications.

Independent reports cite a **Financial Modeling World Cup** benchmark where Claude (deployed via FundamentalLabs' Excel agent) passed 5 of 7 levels and scored **83%** on complex Excel tasks. [1] Take any single benchmark with a pinch of salt, but the direction is consistent: Claude is currently best-in-class on **complex spreadsheet reasoning** specifically.

## Data connectors [1] [2] [4]

The financial-analysis core plugin ships with MCP connectors to:

**Daloopa · Morningstar · S&P Global · FactSet · Moody's · MT Newswires · Aiera · LSEG · PitchBook · Chronograph · Egnyte**

The significance: these are governed, scoped, auditable connections — not a model scraping the web. For a regulated FS firm, that distinction is often what separates "a curiosity" from "a deployable tool". It's also where Claude's offering differs in shape from M365 Copilot, whose strongest integrations are with Microsoft's own surfaces (Excel, Teams, SharePoint, Dynamics 365, Power Platform).

## Deployment surfaces [1] [4]

The same agent templates can run in three different places:

1. **Claude Cowork plugins** — interactive, human-in-the-loop. The agent runs alongside the user, surfaces work for review, and waits for approval at decision points.
2. **Claude Code plugins** — the agent is invoked from a developer's terminal context (relevant when the FS workflow has a code/script component).
3. **Claude Managed Agents** — programmatic, autonomous, API-driven. The agent runs as a service behind the firm's own workflow engine.

The interactive Cowork path is the one most analysts and PMs will see. The Managed Agents path is the one platform teams build on.

## Enterprise controls [1] [2]

Required for serious deployment in our industry, and listed explicitly:

- SSO (SAML / OIDC)
- SCIM provisioning
- Audit logs
- Custom data retention policies
- ISO/IEC 42001:2023 certification (AI management system standard)
- Optional deployment on AWS, Google Cloud, or Azure
- A dedicated FSI solutions team and SI partnerships (Deloitte, Accenture, PwC are named in the Anthropic Partner Network)

## What it isn't

Worth saying plainly so the rest of the pack doesn't oversell:

- It is not a trading system, not a risk engine, not a pricing library.
- It does not replace specialist tooling (Bloomberg terminal workflows, MSCI risk models, internal pricing libraries).
- It is not magic — outputs still require review. Anthropic explicitly positions it as human-in-the-loop, with source attribution on every output so reviewers can verify.

What it is, at the right level of abstraction: **a programmable senior associate** — able to read filings, populate models, draft documents, reconcile accounts, screen KYC files — across the polished output formats (Excel, PPT, Word) the work actually lives in.

---

## Sources

[1] Anthropic — *Agents for financial services* (the May 2026 announcement of the 10 agents). <https://www.anthropic.com/news/finance-agents>
[2] Anthropic — *Claude for Financial Services solutions page.* <https://claude.com/solutions/financial-services>
[4] GitHub — *anthropics/financial-services repository* (Apache 2.0 templates, skills, MCP connectors). <https://github.com/anthropics/financial-services>

---

Next: [`02-how-it-ships.md`](02-how-it-ships.md) — the subscription and access landscape.
