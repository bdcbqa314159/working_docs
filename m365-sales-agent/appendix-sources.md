# Appendix — Sources & verification notes

All claims verified against Microsoft Learn and Microsoft Adoption documentation as of 2026-06-08.

## Primary (Microsoft official) — authoritative

- **Sales agent FAQ** (Microsoft Learn — *the* source for licence / CRM / cloud restrictions).
  <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-m365-copilot-faq>
  Used for: M365 Copilot licence requirement, CRM compatibility (Dynamics 365 Sales / Salesforce Sales Cloud Pro+), GCC/GCC High/DoD exclusion, on-premise CRM exclusion, Bing search behavior, LLM training policy, GDPR compliance.

- **Welcome to Sales agent / Introduction**.
  <https://learn.microsoft.com/en-us/microsoft-sales-copilot/introduction>
  Used for: positioning as a role-based Copilot, Outlook / Teams surfaces.

- **Overview of Microsoft 365 Copilot for Sales — 2026 release wave 1**.
  <https://learn.microsoft.com/en-us/copilot/release-plan/2026wave1/copilot-sales/>
  Used for: current 2026 capability framing, "daily command center", expanded chat capabilities, extensibility direction.

- **Overview of Microsoft 365 Copilot for Sales — 2025 release wave 2** (prior wave for historical context).
  <https://learn.microsoft.com/en-us/copilot/release-plan/2025wave2/copilot-sales/>

- **Lead Research and Outreach overview (preview)** — the autonomous lead agent.
  <https://learn.microsoft.com/en-us/microsoft-sales-copilot/sales-agent-overview>
  Used for: what the autonomous lead-research-and-outreach agent does, data sources (CRM + web + 3rd party), early-access requirement for autonomous engagement.

- **Sales Development agent — autonomously grow qualified pipeline**.
  <https://learn.microsoft.com/en-us/copilot/release-plan/2025wave2/copilot-sales/autonomously-grow-qualified-pipeline-sales-agent>
  Used for: the more-autonomous "AI seller" agent, two-way conversations, qualification → handoff flow.

## "Make a customised pitch" — the documented workflow

- **Sales scenario: Make a customized pitch (Microsoft 365 Copilot)**.
  <https://adoption.microsoft.com/en-us/scenario-library/sales/make-a-customized-pitch-copilot-for-microsoft-365/>
  Used for: the 6-step workflow (Loop → Copilot Chat research → review interactions → PPT slide → Teams recap → Word proposal) — referenced verbatim in `02-scope-and-use-cases.md`.

- **Sales scenario: Make a customized pitch (Copilot for Sales)** — sister scenario for the Sales-agent surface specifically.
  <https://adoption.microsoft.com/en-us/scenario-library/sales/make-a-pitch-copilot-for-sales/>

- **Using Copilot in Sales (Scenario Library index)**.
  <https://adoption.microsoft.com/en-us/scenario-library/sales/>
  Used for: cross-checking what other scenarios are documented.

## CRM-specific

- **Copilot in Dynamics 365 Sales overview**.
  <https://learn.microsoft.com/en-us/dynamics365/sales/copilot-overview>

- **Use Microsoft 365 Copilot in Dynamics 365 Sales (preview)**.
  <https://learn.microsoft.com/en-us/dynamics365/sales/microsoft-365-copilot-chat-in-sales>

- **Copilot for Sales features for Dynamics 365 Sales users**.
  <https://learn.microsoft.com/en-us/microsoft-sales-copilot/features-d365-users>

## Agent ecosystem context

- **AI Agents for Individuals and Businesses** (Microsoft).
  <https://www.microsoft.com/en-us/microsoft-365-copilot/agents>

- **Sales agent — the Copilot agent that speaks sales** (TechCommunity).
  <https://techcommunity.microsoft.com/blog/microsoft365copilotblog/sales-agent---the-copilot-agent-that-speaks-sales/4476894>
  Used for: the practitioner-tone overview that distils what marketing pages describe at length.

- **New sales agents accessible in Microsoft 365 Copilot help teams close more deals, faster** (Microsoft 365 Blog, 2025).
  <https://www.microsoft.com/en-us/microsoft-365/blog/2025/03/05/new-sales-agents-accessible-in-microsoft-365-copilot-help-teams-close-more-deals-faster/>

## Benchmarks

- **Benchmarking AI Quality in Dynamics 365 Sales Qualification Agent** (Microsoft Dynamics 365 Blog).
  <https://www.microsoft.com/en-us/dynamics-365/blog/it-professional/2025/12/11/sales-qualification-agent-benchmarks/>
  Used for: Microsoft's published benchmarks on the qualification agent. Not independently audited — read as Microsoft's published claims.

## What we did NOT verify

- **Whether Sales agent is installed in our office tenant**. This requires checking with IT — see the four checks in `03-fs-fit-and-our-access.md`.
- **Whether our CRM is one Sales agent supports**. Specifically: if we use Salesforce Financial Services Cloud, Sales agent should work on the underlying Salesforce Sales Cloud objects, but the FS-specific objects (Households, Financial Accounts, Goals) may not be in the default tables. We did not verify this end-to-end.
- **Specific contractual data-handling commitments** in our firm's enterprise agreement with Microsoft. The public FAQ describes the default Microsoft posture; enterprise agreements can vary.
- **Whether the autonomous Lead Research and Outreach agent is generally available or still preview** at the time you read this. As of June 2026 it is **preview, with autonomous engagement requiring an early-access form**. Status changes.

## Updating this pack

Quarterly review checklist:

1. Re-check `learn.microsoft.com/en-us/microsoft-sales-copilot/sales-m365-copilot-faq` — has the supported-CRM list expanded? Has the sovereign-cloud exclusion changed?
2. Re-check the release-plan page for the latest wave (`2026wave2`, `2027wave1`, ...) for new capabilities.
3. Re-check whether Lead Research and Outreach has graduated from preview to GA.
4. Update the verified date at the bottom of `README.md`.
