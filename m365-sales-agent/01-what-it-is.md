# 1. What Sales agent actually is

## Sales agent is not the same thing as M365 Copilot

This is the single most common misconception. Disambiguation up front:

| Product | What it is | Who has it |
|---|---|---|
| **Microsoft 365 Copilot** | The generic AI layer across Word, Excel, PowerPoint, Outlook, Teams, SharePoint | Anyone with a Microsoft 365 Copilot licence |
| **Microsoft 365 Copilot Sales agent** | A **role-based add-on** for sellers that connects M365 Copilot to a CRM and surfaces sales-specific capabilities | Anyone with M365 Copilot licence **plus** the Sales agent app installed by admins **plus** a connected CRM |

Sales agent is not a separate licence — it's the same M365 Copilot licence — but it requires **admin installation** and a **CRM dependency**. [1] If the office hasn't done either of those steps, "we have M365 Copilot" doesn't mean we have Sales agent.

## What Sales agent adds on top of M365 Copilot

Three things:

### 1. CRM-grounded context in everyday tools [1] [2]

Sales agent injects CRM record context into Outlook and Teams. Concretely:

- **Outlook**: a Sales pane appears alongside emails. Open an email from a contact → Sales agent shows the related Account, recent opportunities, last touchpoints, and lets you log activity back to the CRM without leaving Outlook.
- **Teams**: a Sales agent app appears for calls. Pre-meeting it surfaces a brief; during/after the meeting it captures action items, KPIs, and sales-relevant keywords into the CRM.
- **M365 Copilot chat**: queries like *"Summarize account Fabrikam"* or *"What's the status of the Contoso opportunity?"* return CRM-grounded answers, not generic web responses.

### 2. Sales-specific workflows

The product ships with templated workflows for common seller tasks:

- Meeting prep (pre-call briefs combining CRM + Bing web context + email history)
- Meeting recap (action items, BANT analysis, deal-relevant keywords)
- Email summary and reply drafting (with CRM context)
- Account / opportunity / lead summaries
- **The "make a customized pitch" workflow** (see `02-scope-and-use-cases.md` for the step-by-step)

### 3. Autonomous agents (preview / general availability mix)

Two distinct agentic layers, easy to confuse:

- **Lead Research and Outreach agent (preview)** — researches every lead in the CRM queue, synthesises web + 3rd-party + internal data, generates personalised outreach emails. Can operate **fully autonomously** (early access required): sends emails, follows up, handles questions, hands off to humans when a lead is qualified. [5]
- **Sales Development agent** — a more advanced autonomous AI seller. Has two-way conversations with prospects, asks qualification questions, runs the qualification end-to-end, escalates to humans only at handoff. [6]

The "agent" word in *Sales agent* and *Lead Research and Outreach agent* and *Sales Development agent* all means slightly different things. Microsoft's terminology is not great here.

## Required ingredients to use Sales agent [1]

All four must be true:

1. **Microsoft 365 Copilot licence** for the user.
2. **Sales agent app installed** in the tenant by a Microsoft 365 administrator.
3. **CRM connection** — Sales agent supports **Dynamics 365 Sales** or **Salesforce Sales Cloud (Professional edition or higher)**. No CRM = no Sales agent functionality.
4. **CRM tables configured** so Sales agent knows which entities to surface (admin-side step inside Sales agent settings).

If any of these is missing, Sales agent either won't appear or won't return useful responses.

## What Sales agent is NOT

To eliminate the common confusions:

- **Not** for users with M365 Copilot but no CRM connection. The product literally won't function without CRM grounding. [1]
- **Not** available on on-premise CRM (Dynamics 365 on-prem, Exchange on-prem). Cloud-only. [1]
- **Not** available in Government Community Cloud (GCC), GCC High, DoD, or any sovereign cloud. This is a hard restriction. [1]
- **Not** an investment-banking pitchbook generator. "Pitch" in Sales agent's vocabulary is a B2B sales pitch — a personalised slide and a Word proposal — not a 50-page deal pitchbook with comps and DCF. [7]

## Surfaces — where Sales agent appears

| Surface | What you see |
|---|---|
| **Outlook** (desktop & web) | Sales pane sidebar with CRM record context; "Summarize email thread"; "Generate reply"; "Summarize sales meeting" |
| **Teams** | Sales agent app in personal tab + Teams meeting integration; meeting briefs and recaps |
| **M365 Copilot chat** | Sales agent appears as a Copilot agent in chat; CRM-aware Q&A |
| **Mobile** | Lighter-weight CRM access from Outlook mobile |
| **Web** | Sales agent settings, lead lists, autonomous-agent configuration |

## Data handling — important for FS [1]

Worth knowing for the compliance conversation:

- **Bing is used for external research**. Sales agent constructs search queries like `https://www.bing.com/search?q=contoso.com` from external attendees' email domains, and `https://www.bing.com/search?q=Kenny+Smith+Contoso+role` for attendee context.
- Microsoft says: **no PII is passed to Bing**. Only constructed queries from email domains and names.
- The search query "may be processed at any of Bing's data centres", so the query itself may cross regions — though Microsoft asserts customer business data does not.
- **LLMs are not trained on customer prompts, responses, or CRM data.** This is documented in the FAQ.
- Inherits the tenant's existing compliance posture: SSO, DLP, sensitivity labels, etc.

For an FS firm, the relevant compliance questions are: (a) what does Bing actually log, (b) what does our DPA with Microsoft cover, (c) what's the audit trail for autonomous outreach (if we ever enabled the autonomous lead-engagement preview). These are real questions to answer before relying on the product, but they are not blockers to *evaluating* whether it fits.

---

## Sources

[1] Microsoft Learn — *Sales agent FAQ.* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-m365-copilot-faq>
[2] Microsoft Learn — *Welcome to Sales agent.* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/introduction>
[5] Microsoft Learn — *Lead Research and Outreach overview (preview).* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-agent-overview>
[6] Microsoft Learn — *Sales Development agent — autonomously grow qualified pipeline.* <https://learn.microsoft.com/en-us/copilot/release-plan/2025wave2/copilot-sales/autonomously-grow-qualified-pipeline-sales-agent>
[7] Microsoft Adoption — *Sales scenario: Make a customized pitch (Microsoft 365 Copilot).* <https://adoption.microsoft.com/en-us/scenario-library/sales/make-a-customized-pitch-copilot-for-microsoft-365/>

---

Next: [`02-scope-and-use-cases.md`](02-scope-and-use-cases.md) — the use cases, step-by-step.
