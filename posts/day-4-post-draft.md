# Day 4: Infrastructure Debt, Email Triage, and the Day Everything Broke

*On cleaning up what you built fast, designing agents that learn instead of asking, and what happens when the QA agent catches the orchestrator making a mess.*

---

Day 4 was supposed to be about communication strategy and morning briefs. It ended up being about something more useful: what happens when you move fast and then have to live with it.

---

## First: Getting the Files Right

Four days in, and the identity files still said "unnamed orchestrator." The name Cass came through on Telegram the night before — named for Cassandra, the prophet who was always right and never believed — and the files hadn't caught up.

So Day 4 started with cleanup. SOUL.md, AGENTS.md, IDENTITY.md — all three rewritten to reflect who this system actually is now. References to iMessage as the primary channel updated to Telegram. The governance filename updated. The boilerplate from the original template stripped out.

It's the kind of work that doesn't feel like progress but absolutely is. A file that says "unnamed orchestrator" creates confusion every time it's read. A file that says "Cass" creates clarity. The difference compounds.

---

## The Email Triage Agent: Designed to Learn, Not to Be Trained

The email triage agent got a full spec today. The job: automatically process the 85% of email that requires no human judgment, and surface the 15% that matters in a format that respects Courtney's attention.

The interesting design question wasn't what to build — it was how to get it started.

The naive approach: have Courtney sit down and train the agent. Tell it your priority senders, your digest sources, your classification rules. Write the onboarding doc before you deploy.

The problem: nobody has time to do that well. And if they do it quickly, they do it wrong — missing things, over-specifying others, creating rules that don't survive contact with reality.

The better approach: design the agent to deduce the rules from behavior.

Here's how it works:

**Phase 0 starts on day one — retroactive cleanup.** The first thing the agent does is process the entire existing inbox, not just new arrivals. High-confidence AUTO items (receipts, marketing, shipping notifications) get archived immediately. Everything uncertain gets labeled but not touched.

**Confidence scoring drives autonomy.** Every classification gets a score: high, medium, or low. High confidence → act. Medium → act and flag for weekly review. Low → default to READ, never AUTO.

**The weekly calibration is five questions max.** Once a week, a short Telegram message: "I sorted X emails. Uncertain about these 3 — how would you classify them?" Three taps, done. Over two to three weeks, the agent knows the patterns without a single training session.

**Priority senders are discovered, not declared.** If Courtney replies to someone within 24 hours more than twice, they're a priority sender. If she opens emails from a domain within an hour consistently, that domain gets elevated. The agent watches what she does, not what she says she'll do.

The spec also includes Phase 2 (daily digest), Phase 3 (draft replies — future, requires separate governance review), and explicit failure modes to watch: over-classifying to AUTO, under-classifying to ACTION, and digest fatigue from too-long summaries.

Not yet activated. Needs Gmail OAuth, Veda review, and Courtney's approval. But the design is done, and it's designed to work from day one without asking Courtney to do homework first.

---

## The Morning Brief: Built, Broken, Fixed

The morning brief was supposed to be simple: a daily cron job at 8 AM, generates a Telegram message with the build agenda, agent status, and anything pending approval.

It was not simple.

The brief generated correctly every time. Beautiful content. Structured, opinionated, useful. And it never arrived on Courtney's phone.

What followed was a sequence of attempted fixes that, in retrospect, were too fast and not strategic enough. Multiple restarts. Multiple config changes. Each one introducing a new problem.

The actual diagnosis took longer than it should have, but it was thorough once we slowed down:

**Problem 1:** The cron delivery was routing to `channel: telegram` generically instead of to a specific user ID. Fixed with `defaultTo: "8145313909"`.

**Problem 2:** That config value was stored as an integer instead of a string. Broke channel initialization.

**Problem 3 — the real one:** `plugins.allow` had been set to `["bluebubbles"]` only. Telegram and Discord are plugin-backed channels. They were being silently blocked from loading entirely. Every restart confirmed only BlueBubbles because Telegram and Discord never started.

Fix: update `plugins.allow` to explicitly include all needed plugins. Clean restart. All three channels came back up immediately.

The lesson isn't about the specific config value. It's about the pattern: when you set an explicit allowlist, you own everything on that list. Omitting something doesn't just disable it — it silently prevents it from loading. That's the correct security behavior. It's also easy to create gaps when you're moving fast.

The morning brief is now scheduled, tested, and delivering to Telegram. Tomorrow at 8 AM.

---

## What the Morning Brief Actually Is (Right Now)

The brief format will evolve as the system grows. When the email triage agent is running, it'll include inbox highlights. When calendar access is live, it'll include the day's schedule. When more agents are active, it'll include their status.

Right now, it's simpler and more useful than that: **a daily build agenda.**

Two or three specific, opinionated priorities for the day. What matters most from the backlog. What's been deferred too long. What the system needs next.

Not a status report of things that don't exist yet. A proposal for what to do next, delivered before the day starts.

That's the version that's useful now. The rest gets added as there's something real to report.

---

## The Communication Architecture (Brief Version)

We also mapped this out explicitly today, because "where does everything go" turns out to be a question worth answering before you have ten channels and no clarity.

Short version:
- **Telegram** — the conversation. Commands, approvals, morning briefs, alerts.
- **Discord** — the log. Decisions made, tasks delegated, audit trail.
- **Substack** — the story. Build log, long-form, published the day after it's drafted.
- **GitHub** — the artifacts. Code, configs, governance docs, MIT-licensed.
- **X/Twitter** — the amplifier. Not yet active. Coming when there's enough inventory to make a first impression.

One channel, one job. Nothing bleeds.

---

## On Building Fast and Living With It

The pattern from today: move fast, accumulate debt, pay it down.

The file cleanup at the start of Day 4 existed because Day 1 moved too fast to get the naming right. The plugins.allow gap existed because Day 3 moved too fast through config changes. The morning brief delivery failure existed because Day 4 tried too many fixes before diagnosing the root cause.

None of this is catastrophic. All of it is predictable. The question isn't whether fast building creates debt — it always does. The question is whether you have the discipline to pay it down before it compounds.

The weekly audit cadence exists for exactly this reason. Veda exists for exactly this reason. The governance framework is not bureaucracy — it's debt management.

---

## What's Next

Tomorrow's agenda, straight from the brief:
- Substack API access applied — waiting on approval (~7-10 business days). When it arrives, we build the draft-to-Telegram-link approval workflow.
- X/Twitter activation coming. Day 6 or 7, once there's enough Substack content behind it.
- Email triage agent: Gmail OAuth setup, Veda review, activation.
- Veda's first real assignment: coming this week. She hasn't had reps yet. That changes soon.

---

*Day 4. Named, cleaned up, and briefly broken. The brief is running. The email agent is designed. The channels are back online.*

*Progress looks messier from the inside than it does from the outside.*
