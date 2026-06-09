# 2. Scope and use cases — what Sales agent actually does

The use cases break into four groups: **CRM-in-flow** (passive, always-on), **assisted workflows** (you trigger; agent helps), **autonomous workflows** (agent runs on its own), and **the "customised pitch" scenario** (which the user asked about specifically).

## Group A — CRM in flow [1] [2] [12]

Always-on, low-friction: Sales agent surfaces CRM data wherever you already are.

| Use case | Where it happens | What you get |
|---|---|---|
| Open an email from a contact | Outlook | Sales pane shows Account, Contact, related Opportunities, recent activity timeline |
| Search CRM record without leaving Outlook | Outlook + Teams | Search bar; embed record as adaptive card in email/chat |
| Log activity to CRM | Outlook + Teams | One-click activity logging without switching apps |
| Ask "What is the status of opportunity X" | M365 Copilot chat | CRM-grounded answer with citations to the record |
| Pre-meeting brief | Teams (before meeting) | Pre-call card combining CRM history + Bing public-web context on attendees |
| Meeting recap | Teams (after meeting) | Action items, BANT analysis, deal-relevant keywords, logged to CRM |

These are the "you didn't ask for it but it's there" capabilities. They're the everyday-utility value of Sales agent — most users get more cumulative time savings from these than from the showier agents.

## Group B — Assisted workflows

You trigger; agent helps. Three of them are highest-value:

### B.1 Summarize email thread / generate reply

In Outlook with the Sales pane open:

1. Open the email thread.
2. Click *Summarize* → Sales agent produces a structured summary with CRM context overlaid (so "Mike said X" is annotated with "Mike is the CFO at the Contoso opportunity worth \$240K, last touchpoint 3 days ago").
3. Click *Draft reply* → reply suggestion using the same CRM context.

Available only for threads >1,000 characters (~180 words). Below that threshold Sales agent assumes there's no useful context to mine. [1]

### B.2 Summarize sales meeting

After a transcribed Teams meeting:

1. Open the meeting in Teams, or open the follow-up email in Outlook.
2. *Summarize sales meeting* → structured recap with action items, KPIs, BANT analysis.
3. *Send recap* → email pre-populated with the recap, ready to send to attendees.

Requires the meeting to have been recorded *with the Sales agent attached to the meeting* AND at least one external attendee saved as a contact in the CRM. [1]

### B.3 Update an opportunity from a meeting

After a meeting:

1. Sales agent surfaces *suggested CRM updates* — proposed changes to the opportunity record based on what was discussed (stage changes, close-date moves, competitor mentions, decision-maker updates).
2. Approve or reject each suggestion.
3. Approved suggestions are logged with provenance (which meeting they came from).

## Group C — Autonomous workflows (preview / early access)

The headline-grabbing part. Two distinct agents:

### C.1 Lead Research and Outreach agent (preview) [5]

What it does autonomously:

- **Researches every lead in the CRM queue** — pulls CRM data, calls web/3rd-party data services, synthesises a per-lead summary.
- **Generates personalised outreach emails** using the synthesised insights.
- **(Optional, behind an early-access form)**: sends those emails, handles replies, follows up, qualifies leads, hands off to a human seller when the lead is "ready".

What an analyst sees, in practice: a list of researched leads in their CRM, each with a synthesised summary (industry, finances, strategic priorities, business challenges, decision-maker validation), each with a pre-drafted personalised email ready to send.

What configuration the admin does:

- Define the lead-research query (which leads to research)
- Define the outreach playbook (email templates, follow-up cadence, qualification criteria)
- Define the handoff criteria (when does the agent stop and pass to a human?)

### C.2 Sales Development agent [6]

A step further than C.1: the autonomous AI seller. Two-way conversations with prospects. Handles FAQs, qualification questions, schedules meetings, escalates only at human-handoff criteria.

This is the most-autonomous offering Microsoft has shipped for sales. Treat it as **forward-looking in regulated FS contexts** — the audit-trail and compliance work it demands is non-trivial.

## Group D — The "make a customised pitch" workflow

The headline use case in this brief. Microsoft documents it as a 6-step scenario. [7] [8]

**Caveat — set expectations**: the "pitch" produced here is a **B2B sales pitch**: a personalised slide deck and a Word proposal, tailored to one customer. It is **not** an IB-style transaction pitchbook. The audience is a customer being sold to, not an internal investment committee.

### The 6 steps, exactly as Microsoft documents them [7]

| Step | Surface | Input | Output | Seller's role |
|---|---|---|---|---|
| 1. Prepare for Discovery | Microsoft Loop | Team collaboration | Brainstormed strategies | Contributor to ideation |
| 2. Research the Company | M365 Copilot Chat | Customer's annual report + CRM data | Summary (e.g. IT spending changes, key initiatives) | Provide documents to analyse |
| 3. Review Interactions | M365 Copilot Chat | Email threads + previous comms | Bulleted notes + call script | Share email history |
| 4. Update Sales Presentation | PowerPoint with Copilot | Customer details from email summary | Personalised slide with industry-relevant visuals | Copy customer info into prompts |
| 5. Summarize Meeting | Teams / Teams Rooms | Meeting recording | Recap with key points + action items | Review transcript |
| 6. Create Proposal | Word with Copilot / Office Agent | Meeting info in prompt | Draft proposal document | Request improvements + refinements |

The output of the workflow: **a personalised PowerPoint slide + a Word proposal document**. Both tailored to one named customer using CRM context and meeting history.

### How long this takes in practice

Microsoft frames it as "minutes per step" — in reality, an experienced seller can run the whole workflow in **1–2 hours** for a customer they already know, perhaps **3–4 hours** for a cold one. The savings vs. building from scratch are real but bounded: this isn't going from a day to ten minutes, it's going from a day to half a day.

### What this is *not* good for

- **Multi-product, multi-stakeholder enterprise pitches** where the deck needs many customer-specific slides — the workflow personalises one slide well, not a full deck.
- **Anything requiring quantitative analysis** — comparisons, ROI models, deal economics. Copilot in Excel does some of this, but it's not part of this workflow.
- **High-design pitchbooks** where the visual quality matters as much as the content — Copilot generates structurally clean but visually average PPT.

## Scope summary — what Sales agent does and doesn't do

### Does well

- CRM-grounded everyday context (emails, meetings, opportunity status)
- Meeting prep + recap, with CRM provenance
- B2B sales pitch personalisation (one customer, one slide, one proposal)
- Lead research (preview): autonomous summarisation of leads with web + CRM data
- Autonomous outreach (early access): hands-off lead engagement until qualified

### Doesn't do (or doesn't do well)

- IB-style transaction pitchbooks (comps, DCF, deal precedents, financing) — wrong shape entirely
- Capital markets / trading workflows — no CRM-driven shape there
- Research analyst notes — analyst output isn't customer-pitched
- Long-context document analysis (300-page filings, 10 transcripts at once) — degrades quickly
- High-design visual outputs — structurally clean, visually average
- Anything on a non-supported CRM, on-premise CRM, or in a sovereign cloud (GCC/GCC High/DoD) [1]

---

## Sources

[1] Microsoft Learn — *Sales agent FAQ.* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-m365-copilot-faq>
[2] Microsoft Learn — *Welcome to Sales agent.* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/introduction>
[5] Microsoft Learn — *Lead Research and Outreach overview (preview).* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-agent-overview>
[6] Microsoft Learn — *Sales Development agent — autonomously grow qualified pipeline.* <https://learn.microsoft.com/en-us/copilot/release-plan/2025wave2/copilot-sales/autonomously-grow-qualified-pipeline-sales-agent>
[7] Microsoft Adoption — *Sales scenario: Make a customized pitch (Microsoft 365 Copilot).* <https://adoption.microsoft.com/en-us/scenario-library/sales/make-a-customized-pitch-copilot-for-microsoft-365/>
[8] Microsoft Adoption — *Sales scenario: Make a customized pitch (Copilot for Sales).* <https://adoption.microsoft.com/en-us/scenario-library/sales/make-a-pitch-copilot-for-sales/>
[12] Microsoft Learn — *Copilot for Sales features for Dynamics 365 Sales users.* <https://learn.microsoft.com/en-us/microsoft-sales-copilot/features-d365-users>

---

Next: [`03-fs-fit-and-our-access.md`](03-fs-fit-and-our-access.md) — where this fits in FS, and what to check about our office access.
