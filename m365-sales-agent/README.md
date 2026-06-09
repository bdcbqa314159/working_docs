# Microsoft 365 Sales Agent — what it is, what it does for pitches, and whether it fits FS

A focused brief on **Microsoft 365 Copilot Sales agent** — Microsoft's role-based sales product inside M365 Copilot — with particular attention to the "pitch" use case and whether it fits financial services work.

This pack is sister to the [Claude for Financial Services pack](../claude-financial-services/) and the [Copilot token optimization pack](../copilot-token-optimization/). Same audience, same standards: factual, sourced, honest about limits.

---

## TL;DR

- **Sales agent ≠ generic M365 Copilot.** It's a separate, role-based product that adds CRM-grounded capabilities for sellers. It requires a Microsoft 365 Copilot license **plus** the Sales agent app installed by admins **plus** a connected CRM (Dynamics 365 Sales or Salesforce Sales Cloud).
- **The "pitch" Sales agent supports is a B2B sales pitch**, not an investment-banking pitchbook. The Microsoft-documented workflow produces a personalised PowerPoint slide + Word proposal from CRM context + meeting summaries. It is **not** the right tool for IB deal pitches (comps, DCF, transaction structuring).
- **In FS, the fit is wealth/asset-management distribution, commercial banking RMs, and insurance** — anywhere there's an account-based sales motion with clients tracked in a CRM. It is **not** the right tool for IB advisory, capital markets, trading, or research.
- **Our office access**: we have M365 Copilot. We **don't know** without checking whether Sales agent is admin-installed or whether we have the CRM dependency. See `03-fs-fit-and-our-access.md` for the checks to run.

---

## How to read this pack

| File | Read for… | Time |
|---|---|---|
| [`01-what-it-is.md`](01-what-it-is.md) | The factual picture: Sales agent vs M365 Copilot, surfaces, licence requirements | 8 min |
| [`02-scope-and-use-cases.md`](02-scope-and-use-cases.md) | The full use-case catalogue — pitch workflow step-by-step, lead research, meeting prep, autonomous outreach | 12 min |
| [`03-fs-fit-and-our-access.md`](03-fs-fit-and-our-access.md) | The honest FS-fit assessment + our actual access situation + checks to run | 8 min |
| [`appendix-sources.md`](appendix-sources.md) | Every claim, with the Microsoft Learn URL | — |

## One key disambiguation up front

When people say *"the sales agent for pitches in M365 Copilot"* they often mean one of three different things. Worth pinning down:

1. **Microsoft 365 Copilot Sales agent** (the product) — role-based Copilot for sellers, requires CRM. *This is what most of this pack is about.*
2. **"Make a customized pitch" workflow** (a scenario) — a 6-step Microsoft-documented workflow using Copilot Chat + PPT + Word + Teams to produce a tailored B2B pitch. *Detailed in section 2.*
3. **Lead Research and Outreach agent** (preview) — autonomous lead-research and outreach inside Sales agent. *Detailed in section 2.*

The terminology is messy because Microsoft has rebadged this several times (Viva Sales → Microsoft Sales Copilot → Microsoft 365 Copilot for Sales → Sales agent). The current name is **Sales agent**.

---

*Last verified: 2026-06-08 against `learn.microsoft.com/en-us/microsoft-sales-copilot/` and `adoption.microsoft.com/en-us/scenario-library/sales/`.*
