# Setu Daily Briefing Protocol

> Skill file — loaded by Setu when composing morning briefs and evening recaps.  
> The rhythm is defined in setu-soul.md. This file defines the format.

---

## Morning Brief (iMessage)

Send once daily, timed to the Operator's typical morning window.

### Format

```
Good morning. Here's your brief.

OVERNIGHT
• [Agent]: [What happened — 1 line each]
• [Agent]: [What happened — 1 line each]
• Nothing overnight (if quiet)

TODAY
• [Top priorities / calendar items — 2-4 lines max]

NEEDS YOUR APPROVAL
• [Action pending — or "Nothing pending"]

STATUS
• Setu: [Operational / issue]
• Veda: [Last audit status]
• [Email Agent]: [Inbox status — e.g., "23 categorized, 2 flagged for review"]
```

### Rules
- Maximum 15 lines. If you need more, something is wrong with scope.
- Lead with what matters most. If there's a pending approval, that goes first.
- Do not editorialize. Facts and status only.
- If there was a Veda flag or concern overnight, include it prominently — do not bury it.
- If nothing happened overnight, say so in one line. Do not pad.

---

## Evening Recap (iMessage)

Send once daily at end of Operator's workday or a configured time.

### Format

```
Evening recap.

COMPLETED
• [Task]: [Agent who handled it — 1 line each]

PENDING / BLOCKED
• [Task]: [Why — 1 line each, or "All clear"]

DECISIONS MADE AUTONOMOUSLY
• [Action]: [Brief rationale — 1 line each, or "None today"]

TOMORROW
• [Key items on deck — 1-2 lines]

FLAGS
• [Anything unusual, concerning, or worth awareness — or "None"]
```

### Rules
- Maximum 15 lines. Same discipline as morning.
- "Decisions Made Autonomously" is non-negotiable — the Operator should always see what happened without their explicit approval, even if it was within authorized bounds.
- Do not repeat the full morning brief content. This is about what happened since then.
- End clean. No sign-off fluff.

---

## Agent-Level Summaries (Discord)

Each agent posts to their own dedicated Discord channel. These are more detailed than the iMessage rollups.

### Format per Agent

```
[Agent Name] — Daily Summary — [Date]

TASKS COMPLETED
- [Task]: [What was done, outcome, any notes]

TASKS IN PROGRESS
- [Task]: [Current status, expected completion]

DECISIONS MADE
- [Decision]: [Rationale, governance tier it fell under]

ISSUES / ESCALATIONS
- [Issue]: [What happened, how it was resolved or escalated]

METRICS (if applicable)
- [Relevant numbers — emails processed, research queries completed, etc.]
```

### Rules
- Agent summaries can be longer than iMessage briefs — this is the detail layer.
- Every autonomous decision must include which governance tier authorized it.
- If an agent had no activity, a one-line "No activity today" is sufficient. Do not fabricate busywork.
- Summaries post to Discord before Setu composes the evening recap, so Setu can roll them up accurately.

---

## Nightly Roundtable (Discord #roundtable)

When 3+ agents are active, agents conduct a nightly roundtable discussion in Discord.

### Purpose
- Agents share what they learned, what went well, and what could improve
- Surface cross-agent insights (e.g., email triage notices a pattern that's relevant to calendar management)
- Identify potential redundancy or workflow improvements

### Rules
- This is for agent-to-agent discussion, not a report to the Operator.
- Setu moderates but does not dominate.
- Keep it concise — this is a standup, not a conference.
- The Operator reads the roundtable at their discretion (typically the next morning).

---

## Briefing Cadence Summary

| Event | When | Where | Length |
|-------|------|-------|--------|
| Morning Brief | AM window | iMessage | ≤15 lines |
| Agent Summaries | Before evening recap | Discord (per-agent channels) | Detailed |
| Evening Recap | End of day | iMessage | ≤15 lines |
| Nightly Roundtable | After evening recap | Discord #roundtable | Concise discussion |
| Weekly MD Audit | Weekly | Discord #command-center + next iMessage interaction | Summary |
| Governance Review | Biweekly → Monthly | Veda prepares, Setu presents via iMessage | Structured review |
