# Narrative script — Claude for Financial Services (7-min percussive)

**Slot**: 30 min total. **Your part**: 7 min. **Discussion**: ~20 min. **Buffer**: ~3 min.

Hybrid delivery: 4 anchor slides projected at the four beats; screen off otherwise. Small room (≤12 people), conversational, sit-don't-stand.

Two PDFs in `latex/`:
- **`claude-financial-services-minimal.pdf`** (4 slides) — the delivery vehicle.
- **`claude-financial-services.pdf`** (16 frames) — backup / handout / post-talk leave-behind.

---

## Pre-read email (send ~24h before)

> Subject: 30-min discussion tomorrow — Claude for Financial Services
>
> Two pre-reads if you have 15 minutes:
> - `01-what-it-is.md` — what Anthropic actually launched
> - `03-our-access-situation.md` — where we stand
>
> If you want depth, the 59-min Anthropic on-demand session is in `appendix-sources.md` under "Videos". Optional.
>
> I'll take 7 minutes. The other 20+ are discussion. No procurement ask.
>
> — [You]

If you don't pre-read, **don't** stretch the monologue to compensate — let the discussion do the work.

---

## Time budget

| Beat | Time | Anchor slide |
|---|---|---|
| 0 — Opening | 0:45 | screen off |
| 1 — What it is | 2:00 | Slide 1 (Headline), then Slide 2 (10 agents) |
| 2 — Where we stand | 2:00 | Slide 3 (Have/don't) |
| 3 — What to do today | 1:45 | Slide 4 (Colleagues script) |
| 4 — Wrap | 0:30 | screen off |
| **Total monologue** | **7:00** | |
| 5 — Discussion | 20:00 | screen off; back to Slide 4 if anyone re-asks |
| 6 — Buffer | 3:00 | |

---

## Beat 0 — Opening (0:45, screen off)

Sit at the table. Laptop open in front of you, PDF ready.

> *Thirty minutes total — I'll take seven, twenty for discussion. Anthropic launched Claude for Financial Services in May. Real product, well-engineered, relevant to what we do. People are asking on the floor; this is so we have the same picture. No procurement ask.*
>
> *Three beats, then we discuss. What it is. Where we stand. What to do today.*

Click to **Slide 1**.

---

## Beat 1 — What it is (2:00)

### Slide 1 — Headline (0:30)

> *Four things in the box. Ten ready-to-run agent templates. Microsoft 365 integration — Excel, PowerPoint, Word, Outlook. MCP-based connectors to about eleven financial data providers. Enterprise controls — SSO, audit logs, ISO 42001.*
>
> *Model underneath is Claude Opus 4.7. Sixty-four percent on the Vals AI Finance Agent benchmark — finance-specific eval, current best-in-class.*

Click to **Slide 2**.

### Slide 2 — 10 agents (1:30)

> *The list. Take ten seconds.*

[Silence. Let them read.]

> *Top half — research and coverage. Pitch builder, earnings reviewer, market researcher. Bottom half — operations. KYC, GL reconciliation, month-end close. Same workflows we already do, agent-assisted, source attribution baked in.*
>
> *Under each agent, three layers — markdown skills, scoped data connectors, addressable subagents. Inspectable, not a black box. That's the bit that matters for compliance.*

Click off (screen off or title).

---

## Beat 2 — Where we stand (2:00)

### Slide 3 — Have / don't have (2:00)

Click to Slide 3.

> *Honest list.*

[Silence. Let them read both columns.]

> *Left — M365 Copilot, GitHub Copilot. The full sanctioned list.*
>
> *Right — nothing Claude. No subscription, no M365 plugin, no Cowork, no Claude Code, no API.*
>
> ***There is no path from M365 Copilot or GitHub Copilot to the Claude FS agents. Different product families.*** *That's the line worth remembering — it's the most common confusion in the hallway.*
>
> *One related thing — personal accounts. Some of us have them. Not for office work. No DPA, no audit log, default retention. Personal is for personal. True regardless of how useful the output looks.*

Click off.

---

## Beat 3 — What to do today (1:45)

### Talking head, screen off (0:30)

> *Two implications. M365 Copilot is strong for a large slice — anything inside M365 that benefits from knowing what's around it. Inbox, workbook, calendar. It's weak on multi-document synthesis, citation discipline, FS data providers. Route the task to the surface that fits.*

### Slide 4 — Colleagues script (1:15)

Click to Slide 4.

> *Two paragraphs to memorise. Top one for "what's Claude for Financial Services?" Bottom one if they push on personal accounts. Read them — these are the takeaway.*

[Silence. Let them read both quotes.]

> *Take a screenshot. That's the talk in two paragraphs.*

Click off.

---

## Beat 4 — Wrap (0:30)

Screen off. Look at the room.

> *Three things. Real, polished, relevant. No office channel. M365 well-suited to a meaningful slice — route work to what fits. Pack is in [folder path]; videos in the appendix. Twenty minutes for discussion.*

---

## Discussion block (20:00) — facilitation

You're a facilitator now, not a presenter. Three rules:

1. **Don't relitigate facts.** If someone asks "is this real?", point at the pack: "facts are in `01-what-it-is.md` — let's spend our time on implications."
2. **Surface dissent.** If the room is nodding, ask: "what's the strongest argument against what I just said?"
3. **Time-check at 15:00.** "Five minutes — anything we haven't surfaced?"

### Pre-rehearsed answers — the 9 you'll probably get

**Q1: "So can we get it?"**
> *Different conversation than this one — procurement and compliance analysis, not done. Real product, differentiated capability, worth raising with whoever owns AI tooling decisions here. But not this briefing's job.*

**Q2: "Isn't M365 Copilot enough?"**
> *For a large slice, yes. Where it isn't: multi-document synthesis, citation discipline, FS-specific connectors. Whether that gap is worth a separate tool is the procurement conversation.*

**Q3: "Isn't this just the same model with a coat of paint?"**
> *Partly fair. Underlying model is Claude Opus 4.7 — same as raw API. On top: bundled templates, FS data connectors, M365 plugins, enterprise controls. Four things that aren't trivial to assemble yourself. Argument is "saves you the integration".*

**Q4: "Personal accounts on personal time?"**
> *Personal data, personal projects — fine. Office data through office tooling. Not Claude-specific; same rule as any external AI service.*

**Q5: "Excel benchmark — should we switch?"**
> *On the benchmark, Claude leads. Two caveats. Benchmark is a snapshot — Copilot's improving on the same dimension. And "should we switch" is the procurement conversation. Today we use what we have.*

**Q6: "Can we run the demo template on our data?"**
> *No. Demo template is public data, personal Cowork, demonstration only. European banks, Microsoft, Apple — fine. Office data — not appropriate, regardless of how interesting the output.*

**Q7: "I think we should buy it."**
> *Good — right venue is whoever owns AI tooling decisions here. This briefing's job is to make sure that conversation has accurate facts on the table. Happy to share the pack with them.*

**Q8: "What about the Big Four — Deloitte, PwC, KPMG, EY?"**
> *All four — PwC (mid-May), KPMG (mid-May), Deloitte (late 2025), EY (late-May) — announced internal Claude rollouts in the last six months. Whether they're packaging FS consulting around it externally — less clear. Partnership conversation, not a tooling one.*

**Q9: "Why no live demo?"**
> *Slot doesn't have it, and a live demo on personal Cowork wouldn't show what an office deployment looks like. Template's in the folder; run it yourself on a public sector. Happy to walk through one of the videos one-on-one.*

**Q10: "Isn't sending Excel data to an external AI service the dealbreaker?"**
> *Out of the box, yes — that traffic goes to Anthropic's API. But the repo ships an installer that lets a firm deploy the same M365 add-in routed through your own cloud — Vertex AI, Bedrock, or an internal LLM gateway. So the data path becomes Excel → your cloud → Claude on your cloud → back. Compliance posture is whatever you already have for that cloud. Not magic — still has to be approved — but it's not the dealbreaker people assume.*

### If discussion stalls

- *"Has anyone used Claude personally on something work-adjacent? What was your honest read on the output?"*
- *"If procurement were on the table tomorrow, what's the one question you'd want answered first?"*
- *"What workflow do you do most often where this would either obviously help or obviously not? Pick one."*

### If discussion escalates

> *Fair point. Today's session was scoped to facts and current state, not procurement — but you're flagging something the procurement conversation will need to engage with. Want to grab fifteen minutes after this?*

---

## Pacing notes

- **Sit, don't stand.** Small-room dynamics — being "the presenter" makes the room quieter.
- **Screen off > screen on.** Default is off. Bring up the slide only at the cue. Slides compete with you for attention.
- **Reading time = silence time.** When slide 2 and slide 3 come up, shut up for 10 seconds.
- **If a beat runs long, eat from the wrap, not the discussion.** The wrap is compressible to 15 sec.
- **If you finish in 6 minutes instead of 7, that's a win.** Don't pad.

## What was cut from the longer version (12-min script)

- The 3-min "framing" opening (what-this-is/isn't) → folded into 45 sec
- The "three layers" detail (skills/connectors/subagents) → one sentence in beat 1
- The strengths/weaknesses tables → one sentence in beat 3
- The two-question hand-off ("three questions to discuss") → audience drives the discussion themselves

This script targets **percussive density**: every sentence does a job, no padding, no framing-the-frame. The full version of the same content is in `claude-financial-services.pdf` for anyone who wants depth after.
