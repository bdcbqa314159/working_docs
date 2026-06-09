# Appendix — Sources & verification notes

Every non-obvious claim in this pack is grounded in one of the sources below. Verified 2026-06-08.

## Primary (official GitHub) — authoritative

- **Models and pricing for GitHub Copilot** — the rate card.
  <https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing>
  Used for: every per-model token price in `01-new-billing-model.md`.

- **GitHub Copilot is moving to usage-based billing** (GitHub Blog announcement).
  <https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/>
  Used for: effective date (1 June 2026), AI Credit allowances per plan, what stays free, official rationale.

- **Plans for GitHub Copilot** (GitHub Docs).
  <https://docs.github.com/en/copilot/get-started/plans>
  Used for: plan pricing.

- **VS Code Copilot FAQ**.
  <https://code.visualstudio.com/docs/copilot/faq>
  Used for: confirming reference to optimization guidance, model picker behavior.

## Legacy (still relevant for annual subscribers)

- **Model multipliers for annual plans on request-based billing (legacy)**.
  <https://docs.github.com/en/copilot/reference/copilot-billing/model-multipliers-for-annual-plans>
  Notes: still applies to Pro / Pro+ annual subscribers who paid before 1 June 2026, until their term expires. Multipliers were raised on 1 June for those users.

- **Overview of request-based billing (legacy)**.
  <https://docs.github.com/en/billing/concepts/product-billing/github-copilot-premium-requests>
  Used to describe what the old system was.

## Community & practitioner

- **Community discussion #163104 — How to Optimise and Reduce Your Copilot Premium Request Usage**.
  <https://github.com/orgs/community/discussions/163104>
  Used for: chained-prompt patterns, conversation continuity tactics, model-quality observations.

- **SmartScope — Copilot premium request optimization: 8 anti-patterns**.
  <https://smartscope.blog/en/generative-ai/github-copilot/github-copilot-premium-request-optimization/>
  Used for: the named anti-patterns ("prompt-chipping", "agent-mode-as-chat", high-multiplier confirmations), the two-lane workflow framing, `.github/copilot-instructions.md` and `.github/prompts/` guidance.
  Note: the article was written under the legacy multiplier system; the framings translate cleanly to the token system since the *underlying* cost shape is the same (cheaper models cost less; more context costs more).

- **Alessio Franceschelli — Stop wasting premium requests: the ask tool trick**.
  <https://alessio.franceschelli.me/posts/ai/stop-wasting-premium-requests-in-github-copilot/>
  Used for: the "ask tool" pattern in agent mode.

- **GitHub Blog — Changes to GitHub Copilot Individual plans**.
  <https://github.blog/news-insights/company-news/changes-to-github-copilot-individual-plans/>
  Background context for the transition.

## Industry coverage (context, not authoritative)

- TheRouter.ai, ChatForest, DEV Community, prodSens, AI Tool Briefing, TechJournal, Medium reports — all documented the user-reported cost spikes (10×–50× in extreme cases, \$30–40 agentic sessions). Used for the public-reports framing in `01-new-billing-model.md` and the deck.

## What we did NOT verify

- The exact retrieval mechanism behind `@workspace` / `#codebase` is not fully documented; the cost characterisation in `02-vscode-surfaces.md` is based on observable behaviour ("retrieved subset of files, larger than `#file:`") rather than a published spec.
- The "10% Auto discount" mentioned in legacy-era optimization writing applied under the multiplier system. Whether an equivalent routing-driven saving exists under token billing isn't explicitly documented; treat Auto's benefit under the new system as "sensible default selection" rather than a quantified discount.
- Per-surface tool-call output handling in Agent mode (whether prior tool results are summarised or fully re-injected) is implementation-defined. Our claim that "tool output stacks" reflects user-observable cost behaviour — it's the right mental model for budgeting, even if internally there's some history compression.

## Updating this pack

When GitHub publishes a new rate-card revision:

1. Re-fetch `docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing` and update `01-new-billing-model.md`'s tables.
2. Re-check the blog news feed at `github.blog/news-insights/company-news` for any new pricing announcements.
3. Update the verified date at the bottom of `README.md` and `04-cheatsheet.md`.
