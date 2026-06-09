# Appendix — Sources & verification notes

All claims in this pack are grounded in the sources below. Verified 2026-06-08.

## Primary (Anthropic) — authoritative

- **Agents for Financial Services** (Anthropic, May 2026 announcement of the 10 agents).
  <https://www.anthropic.com/news/finance-agents>
  Used for: the 10 agent template names, what each does, "skills + connectors + subagents" structure, deployment surfaces (Cowork / Claude Code / Managed Agents), enterprise controls list.

- **Claude for Financial Services solutions page**.
  <https://claude.com/solutions/financial-services>
  Used for: value-prop framing, named use cases (IB, commercial banking, asset management, insurance), public list of data providers and integrations.

- **Advancing Claude for Financial Services** (Anthropic blog).
  <https://www.anthropic.com/news/advancing-claude-for-financial-services>
  Used for: context on the FS programme's evolution.

- **anthropics/financial-services** (open-source repo).
  <https://github.com/anthropics/financial-services>
  Used for: Apache 2.0 licence confirmation, directory structure (agent-plugins, vertical-plugins, MCP connectors, managed-agent cookbooks), the install-via-CLI workflow, the fact that templates can be deployed via Managed Agents API or as Cowork plugins.

- **Install financial services plugins** (Claude Help Center).
  <https://support.claude.com/en/articles/13851150-install-financial-services-plugins>
  Used for: subscription tier requirements for plugin installation.

- **Claude for the financial industry — practical deployment guide** (Anthropic PDF).
  <https://www-cdn.anthropic.com/files/4zrzovbb/website/34783bca828d7fa331f515ced26f1c9232151b2c.pdf>
  Used for: enterprise deployment considerations.

## Pricing & plan structure

- **What is the Enterprise plan?** (Claude Help Center).
  <https://support.claude.com/en/articles/9797531-what-is-the-enterprise-plan>

- **What is the Team plan?** (Claude Help Center).
  <https://support.claude.com/en/articles/9266767-what-is-the-team-plan>

- **Claude Enterprise pricing in 2026** (Runbear analysis — mid-market context).
  <https://runbear.io/posts/claude-enterprise-pricing-mid-market>
  Used for: the "headline $20 base + token consumption billed separately" framing.

- **Claude pricing in 2026** (Finout overview).
  <https://www.finout.io/blog/claude-pricing-in-2026-for-individuals-organizations-and-developers>
  Used for: cross-referencing pricing claims.

## Benchmarks & performance claims

- The **64.37% on Vals AI Finance Agent benchmark** figure is reported in multiple secondary sources tracing to Anthropic's announcement. Treat as Anthropic's published number, not independently audited.

- The **83% on complex Excel tasks** and **5 of 7 levels of Financial Modeling World Cup** are reported via FundamentalLabs' Excel agent benchmarks, cited in Anthropic's announcement.

## Comparison / context

- **Microsoft 365 Copilot vs Claude Enterprise** (Microsoft's own comparison page).
  <https://www.microsoft.com/en-us/microsoft-365-copilot/copilot-vs-claude-enterprise>
  Note: this is Microsoft's framing, not neutral. Used carefully for understanding how Microsoft positions the choice.

- **Claude vs Copilot for Excel** (Ninetwothree).
  <https://www.ninetwothree.co/blog/claude-vs-microsoft-copilot-for-excel>
  Used for: independent observations on the Excel-specific comparison.

- **ChatGPT vs Copilot vs Claude for Finance** (Prime AI Solutions, 2026 edition).
  <https://www.primeai.solutions/blog/chatgpt-vs-copilot-vs-claude-finance>
  Used for: industry framing.

- **Enterprise Showdown: Claude vs Copilot** (Netcom Learning).
  <https://www.netcomlearning.com/news/artificial-intelligence/enterprise-showdown-claude-vs-copilot>
  Used for: industry framing.

## Videos — further viewing

**On-topic for the May 2026 launch** (the 10-agents + M365 + Moody's partnership release this pack documents):

- **The Briefing: Financial Services** — Anthropic virtual event, 5 May 2026, 11:00–12:30 EST. Keynote with Anthropic executives + customer institutions sharing real deployments. The launch event itself.
  <https://www.anthropic.com/events/the-briefing-financial-services-virtual-event>
  *Best for*: the audience that wants to hear the announcement narrative from Anthropic's leadership directly.

- **Claude for Financial Services: Putting agents to work** — Anthropic webinar, 7 May 2026. Practitioner-focused, with live demos on representative deal-side and operations tasks.
  <https://www.anthropic.com/webinars/claude-for-financial-services-putting-agents-to-work>
  *Best for*: the audience that wants to see the agents actually doing work, not just hear about them.

- **Claude for Financial Services teams: Putting agents to work (on-demand recording)** — 59 minutes, Goldcast. Hosted by Nick Lynn (Anthropic Head of Product for FS) and Owen Scully (Applied AI Team Lead).
  <https://anthropic.ondemand.goldcast.io/on-demand/74ae0fc7-f591-442f-8fe1-244f409c1fb5>
  *Best for*: most useful single resource for someone wanting depth in one sitting. Pre-read candidate if you go that route.

**Earlier context** (Jul–Oct 2025 — these document the *initial* Claude for Financial Services release, which preceded the May 2026 10-agent expansion):

- **Claude for Financial Services Keynote** — Anthropic, 17 Jul 2025. The original launch keynote.
  <https://www.youtube.com/watch?v=5zd7m3Rh5B0>

- **How Claude is transforming financial services** — Anthropic, 27 Oct 2025. Mid-cycle update with executives breaking down adoption patterns.
  <https://www.youtube.com/watch?v=a8PmR-fNQ_0>

  *Use carefully*: cite as "context for the FS programme's trajectory", not as documentation of the May 2026 10-agent release.

**What I did NOT find** (search ran 8 June 2026):

- No standalone Deloitte / Accenture / PwC / EY / KPMG demo videos showing Claude FS agents in a partner-delivered context. The Big Four–Anthropic partnerships (PwC's "Office of the CFO", Deloitte's 470k-seat deployment, KPMG's 276k-seat rollout) are documented in news coverage and press releases, not in published demo videos.
- No verified Bloomberg Television clip of the launch I was confident enough to link — the YouTube page returned only structural content on fetch, so I couldn't confirm the specific video's title and date.

If a partner demo video surfaces later (Anthropic Partner Network events, conference sessions, customer case-study videos), add it under "Earlier context" or upgrade to "On-topic" if it's specifically about the 10-agent release.

## What we did NOT verify

- **Specific Anthropic-quoted token discounts** that may apply to Claude Enterprise contracts via direct procurement negotiation. The publicly listed pricing is what we used; bespoke enterprise deals can differ.
- **The exact set of MCP connectors available in production** vs. the ones listed in the public repo. The repo lists 11 connectors; specific configurations / availability per region may differ.
- **Specific compliance certifications beyond ISO/IEC 42001:2023** — Anthropic may publish additional certifications (SOC 2 Type II, etc.) that we did not enumerate here.
- **Our office's specific GitHub Copilot and M365 Copilot SKUs** — quoted comparisons (e.g. M365 Copilot at ~\$30/seat) are at the standard enterprise SKU level. Our specific contractual pricing may differ.

## Updating this pack

Things move fast in this space. Quarterly review checklist:

1. Re-fetch `anthropic.com/news/finance-agents` — has the agent count or surface mix changed?
2. Re-fetch `claude.com/solutions/financial-services` — new integrations? changed pricing?
3. Re-fetch the github repo — new agents or skills added?
4. Re-fetch the Microsoft comparison page — Microsoft's framing tells us how the competitive landscape is shifting.
5. Update the verified date at the bottom of `README.md`.
