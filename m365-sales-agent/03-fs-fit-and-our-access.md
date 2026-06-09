# 3. FS fit and our access situation

Two questions answered here:

1. **Does Sales agent fit FS work?** Honest answer with the segments mapped out.
2. **Do we have access?** What we know, what we don't, and the checks to run.

---

## Question 1 — Where Sales agent fits in FS

Sales agent is built for a **B2B sales motion against named accounts tracked in a CRM**. That description fits some FS lines of business well, and others not at all.

### Strong fit — segments where Sales agent is genuinely useful

| FS segment | Why Sales agent fits | Typical use |
|---|---|---|
| **Wealth management / private banking distribution** | Client-by-client sales motion, relationship continuity matters, CRM-tracked | Meeting prep before HNW client reviews; tailored investment-product pitches; follow-up summaries |
| **Asset management institutional distribution** | Selling funds/mandates to RIAs, pensions, family offices; long sales cycles | Lead research on prospect institutions; pre-meeting briefs; RFP response drafting |
| **Commercial banking RMs** | Multi-product cross-sell to corporate clients; CRM is the operating system | Pre-meeting briefs for client visits; tailored credit/treasury proposals |
| **Insurance distribution (broker / agent / corporate insurance)** | Per-customer policy structuring + renewal cycle | Renewal-prep briefs; tailored coverage proposals |
| **Capital markets sales (DCM / ECM origination — soft fit)** | Account-coverage workflow exists, though deal-specific work needs other tools | Coverage prep for issuer meetings; CRM-based call-pattern tracking |

The common shape: **a known customer, tracked in a CRM, with a multi-touch sales cycle, where context from past interactions improves the next conversation**.

### Poor fit — segments where Sales agent is not the answer

| FS segment | Why Sales agent doesn't fit | Better tool |
|---|---|---|
| **Investment banking advisory (M&A pitchbook generation)** | The "pitch" Sales agent supports is one personalised slide + a Word proposal. IB pitchbooks are 30-50 PPT slides of comps, DCF, precedents, financing — different artifact entirely | Bespoke build in Excel + PPT; Claude FS *Pitch Builder* agent if available |
| **Trading / market-making / execution** | No "named-account sales motion"; the work is execution, not pitching | Trading systems, not Sales agent |
| **Research analysts** | Output is research notes for many subscribers, not tailored proposals to one customer | Standard research tooling |
| **Quant / strats / risk modelling** | Quantitative work, no CRM-driven workflow | Bespoke models, not Sales agent |
| **Risk management / treasury / ALM** | Internal-facing analytical work, no sales motion | Internal analytical tooling |

### A precise way to say it

> *Sales agent fits the parts of FS where the operating system is the CRM and the deliverable is a per-customer pitch or proposal. It does not fit the parts of FS where the operating system is Excel + market data terminals and the deliverable is an analytical artifact.*

In a universal bank, that means: **wealth, AM distribution, commercial banking, insurance distribution → yes**. **IB advisory, trading, research, quant → no**.

## Question 2 — Our office access situation

We know we have **Microsoft 365 Copilot**. We do *not* know — from outside — whether we have **Sales agent**. The two are related but not equivalent.

### What "having M365 Copilot" tells us, and doesn't [1]

Having M365 Copilot means the underlying licence exists. But Sales agent additionally requires:

1. The **Sales agent app installed** by a Microsoft 365 administrator in our tenant.
2. **A CRM connection** to Dynamics 365 Sales or Salesforce Sales Cloud (Pro+).
3. **CRM tables configured** so Sales agent knows what to surface.

Any of those being missing → Sales agent either doesn't appear or doesn't return useful answers. Common scenarios:

- We have M365 Copilot but no CRM → Sales agent unusable.
- We have M365 Copilot and a CRM, but Sales agent isn't installed → Sales agent unavailable.
- We have M365 Copilot, a CRM, and Sales agent installed, but only a subset of users are licensed/enabled → most colleagues won't see it.

### Checks to run

Before we make any claim about access in a team conversation, four things to verify:

1. **Is Sales agent installed?**
   In Outlook desktop, look for the Sales pane in the right sidebar (or *Sales* in the app launcher). In Teams, look for *Sales* in the left navigation. If absent on a sample of seats, it's not installed.

2. **What CRM do we use?**
   If we use **Salesforce** or **Dynamics 365 Sales** for client tracking → Sales agent can in principle connect. If we use a proprietary CRM (Murex client module, Bloomberg AIM, Salesforce Financial Services Cloud, Wealthbox, Avaloq client, internal CRM) → Sales agent does not support those out of the box.
   - **Salesforce Financial Services Cloud (FSC)** is the most common "fit" case. It runs on Salesforce Sales Cloud underneath, so Sales agent *should* work, but the FS-specific objects (Households, Financial Accounts, Goals) may not be in the surfaced tables by default.

3. **What's our cloud?**
   If we're in **US GCC, GCC High, DoD, or any sovereign cloud** — Sales agent is **explicitly unsupported**. [1] This is a hard restriction. EU public cloud is supported.

4. **What's our subscription posture?**
   M365 Copilot licences are per-user. If only a subset of the office has M365 Copilot, only that subset *could* use Sales agent.

### What to say if a colleague asks "can we use Sales agent today?"

A clean answer:

> *"We have M365 Copilot, but Sales agent is a separate add-on — it requires admin install and a CRM connection (Dynamics 365 Sales or Salesforce). We need to confirm with IT whether Sales agent is enabled in the tenant and whether our CRM is one it supports. If both are true, the strongest fit in our context is [wealth / AM distribution / commercial banking / insurance distribution — pick the segment your colleague is in]. It is not the right tool for IB pitchbooks or trading workflows."*

## Comparison table — Sales agent vs. the alternatives for FS pitch work

For completeness, including the Claude FS *Pitch Builder* for the IB use case:

| Capability | M365 Copilot (generic) | M365 Sales agent | Claude FS Pitch Builder |
|---|---|---|---|
| CRM grounding | ❌ | ✅ (Dynamics / Salesforce) | ❌ |
| Customer-specific B2B pitch (1 slide + proposal) | Partial | ✅ | Partial |
| IB-style pitchbook (comps, DCF, precedents) | ❌ | ❌ | ✅ |
| Lead research + autonomous outreach | ❌ | ✅ (preview) | ❌ |
| Meeting prep with CRM context | ❌ | ✅ | ❌ |
| Excel-deep modelling | Partial | Partial | ✅ |
| Long-context document synthesis | Limited | Limited | ✅ |
| **Our office access today** | ✅ | ❓ (verify) | ❌ |

The honest picture: there's no single tool that covers every pitch shape in FS. Sales agent (if we have it) covers the **distribution / RM / wealth** flavour of pitch well; Claude FS Pitch Builder covers the **IB advisory** flavour of pitch well; nothing covers both.

## Recommended next steps

1. **Confirm with IT** whether Sales agent is admin-installed in our tenant. (~5 min email.)
2. **Confirm the CRM**: which CRM the office uses for client tracking, and whether Sales agent supports it.
3. **If yes on both**: pilot the "make a customised pitch" workflow on a real non-sensitive opportunity, and assess whether the output quality justifies promoting it to the wider team.
4. **If no on either**: nothing more to do. The pack documents what Sales agent is so people asking get an accurate answer; we're not lobbying for procurement.

---

## Sources

[1] Microsoft Learn — *Sales agent FAQ* (licence, CRM, cloud restrictions). <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-m365-copilot-faq>

---

Next: [`appendix-sources.md`](appendix-sources.md).
