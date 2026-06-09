Claude for Financial Services — briefing bundle
=================================================

What this is
------------
A self-contained pack about Anthropic's Claude for Financial Services launch
(5 May 2026), our access situation, and what to do about it today. The pack
was produced and is being shared internally; it is informational and contains
no procurement ask.

Contents
--------
1-handout.pdf
    The 2-page A4 takeaway. The single sheet to read if you only have 5
    minutes. Page 1: what was launched, the 10 agents, the 3 access paths,
    what we have / don't have. Page 2: the two-paragraph script for
    answering colleagues, the personal-accounts boundary, a 10-question
    FAQ, and pointers to further reading.

2-example-european-banks.pdf
    An example of what one of the FS agents actually produces. A sector
    intel pack on European banks, generated via the Market Researcher
    agent in a personal Claude Cowork instance on public data. ~5 pages,
    fully sourced. Read it to calibrate what "agent output" means in this
    product — it is not a chat transcript.

3-prompt-template.md
    The prompt template that produced the artifact in (2). Two invocation
    patterns (agent-orchestrated and skill-direct), the paste-ready
    European banks block, and four refinement turns. Anyone with personal
    Cowork access can run this on a different public sector to produce
    an equivalent artifact.

4-presentation-slides.pdf
    The 4-slide minimal deck used at the briefing meeting. For reference
    if you missed the session or want to flip back to the colleagues
    script on slide 4.

source/
    The underlying markdown reference files used to assemble everything
    above. Read these if you want depth on a specific topic:
      - 01-what-it-is.md           : the offering in detail
      - 02-how-it-ships.md         : subscription tiers, paths, BYOC routing
      - 03-our-access-situation.md : the honest articulation of where we stand
      - 04-what-we-can-do-today.md : pragmatic guidance with M365 + GitHub Copilot
      - appendix-sources.md        : every claim, sourced; videos; what we
                                     did not verify

How to read it
--------------
- For a 5-minute orientation: read 1-handout.pdf.
- For a tangible sense of the capability: read 2-example-european-banks.pdf.
- To run an equivalent artifact yourself: 3-prompt-template.md.
- For depth on the briefing: source/01-what-it-is.md, then
  source/03-our-access-situation.md.
- For citations and videos: source/appendix-sources.md.

Boundary
--------
The example in 2-example-european-banks.pdf was produced via a personal
Cowork instance on public data, for office demonstration only. It is not
produced using office tooling or office data, and the personal-account
data-handling posture is materially different from a sanctioned office
deployment — direction-of-capability only, not deliverable quality at our
compliance standard.

If you run the prompt template in (3) yourself, the same boundary applies:
public targets only, personal Cowork instance only, demonstration only.

Verification
------------
All claims verified against:
  - anthropic.com/news/finance-agents
  - claude.com/solutions/financial-services
  - github.com/anthropics/financial-services
as of 8 June 2026. See source/appendix-sources.md for the full citation list.
