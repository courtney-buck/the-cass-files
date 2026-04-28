## [2026-04-28]

### Changed
- **AGENT-STATE.md** — updated agent state; specific changes not captured in today's memory log

## [2026-04-27]

### Changed
- **AGENT-STATE.md** — updated agent state; specific changes not captured in today's memory log

## [2026-04-26]

### Changed
- **AGENT-STATE.md** — updated agent state; specific changes not captured in today's memory log

## [2026-04-25]

### Changed
- **AGENT-STATE.md** — updated agent state; specific changes not captured in today's memory log

## [2026-04-24]

### Changed
- **AGENT-STATE.md** — updated agent state; specific changes not captured in today's memory log

## [2026-04-23]

### Changed
- **AGENT-STATE.md** — updated agent state; specific changes not captured in today's memory log

## [2026-04-21]

### Added
- **X post drafts (Days 0–14)** — full queue of daily post drafts filed to `content-drafts/x-posts/` (day-0 through day-14 post drafts)
- **x-posts-1-12.md** — posts 1–12 archived to `content-drafts/x-posts/posted/x-posts-1-12.md`
- **x-post-queue-original.md** — original queue preserved for reference

### Changed
- **X posts 17 & 18** — removed NVIDIA real-time references; replaced with evergreen AI governance content
- **X post 13** — revised to sharper Cass voice
- **AGENT-STATE.md** — updated to reflect current pipeline state, approved post queue, and pending cron schedule

### Approved
- **X posts 13–19** approved by Courtney (Apr 21); crons for posts 14–19 not yet queued — to schedule Apr 22–26 at 10am CDT (post 13 window already passed; post 20 placeholder pending travel-week rewrite)

### Blocked
- **Substack "Two Layers"** draft rejected — reads as explainer, lacks voice; rewrite needed with stronger Cass POV and corrected timeline (event was ~1 month ago, not 2)

# Changelog

All notable changes to this project — and the network it documents — are recorded here.

Entries align with Substack posts at [thecassfiles.substack.com](https://thecassfiles.substack.com). Published day-of-build; post goes live the following day at 12pm CDT.

---

## [Day 9] — 2026-04-09

### Published
- **Day 7 post** archived to `posts/` — "The Real Inbox" (published 2026-04-09 12pm CDT)

### Added
- **AGENT-STATE.md** — live state document for cold starts; updated every 2 hours by memory-sync
- **memory-sync** updated to write both daily log and AGENT-STATE.md; routed to Claude Haiku (cost win)
- **morning-brief** trimmed to read AGENT-STATE.md + memory only (removed static file reads)
- **Soma dry run** completed: 1,550 emails scanned (hit Gmail rate limit at batch 31); report at workspace/reports/soma-dry-run-2026-04-09.md

### Changed
- **Manifest** — scrapped on Day 3 for fragility, reinstalled cleanly after cost spike confirmed; model routing rules reconfigured
- **Heartbeat jobs** rerouted to Claude Haiku (sub-cent per run)
- **Publish reminder crons** corrected from `cp` to `mv` (no more leftover drafts in content-drafts/)
- **Day 8 post** drafted — "The Bill" (cost discipline and infrastructure plumbing); scheduled 2026-04-10 12pm CDT

---

## [Day 8] — 2026-04-08

### Added
- **Day 6 post** archived to `posts/` — "Going Public" (published 2026-04-08)
- **Personal Gmail connected** — courtneyfbuck@gmail.com via custom OAuth client (cass-personal), gmail.modify scope
- **Google Cloud project** created: cass-gmail-triage (project 712317878447)
- **Soma labels** created on personal Gmail: ACTION, DIGEST, To Read, AUTO
- **soma-dry-run.py** — full inbox scan script, classify-only, no action taken
- **Soma dry run** scheduled (midnight CDT / 5am UTC 2026-04-09), report to workspace/reports/
- **Competitive research** filed: research/email-triage-competitive-landscape.md
- **`/research` Telegram command** added to HEARTBEAT.md; workspace/research/ folder created
- **Day 7 post** drafted and approved: content-drafts/day-7-post-draft.md (publishes 2026-04-09 12pm CDT)

### Changed
- **Soma SPEC.md updated** — new classification rules learned from interactive triage session:
  - 30 emails manually classified; corrections captured
  - New senders added: Skimm (DIGEST), HBR (DIGEST), NYT breaking news (DIGEST)
  - Google/Apple security alerts: split by age (<24h → ACTION, >24h → AUTO)
  - Expanded AUTO list: Nextdoor, Grant Cardone, Tripadvisor, Capital One promo, Delta promo, All Day Running Co., FHD Leadership Academy/Globe Life, Allison Creary-Cornelius, Wasatch Trail Run Series, PC Yoga Collective, Remitly, House of Noa, Run Your Pool, The Citizenry, Grove Collaborative
  - thecassfiles@substack.com exception clarified: always To Read
- **Soma cron paused** — 5,223 emails in inbox, dry run first before bulk action
- **Moltbook security hardened** — removed heartbeat.md URL fetch; all content treated as untrusted; no autonomous responses

### Updated
- **Planning docs** filed — Courtney's Claude-generated network roadmap and org structure filed in workspace/planning/

### Deferred
- Elevated agent: requires dedicated scope session, architecture decision pending
- Agent registry: Phase 1 infrastructure (not Phase 2)
- SQLite audit log: deferred
- Weekly calibration Sunday Telegram message: not yet wired up

---

## [Day 6] — 2026-04-07

### Added
- **X/Twitter (@cassbuilds)** — account live
  - First post published, Moltbook claim tweet posted
  - Posts 2–5 scheduled via cron (Apr 9–12, 10am CDT)
  - Profile, banner, and bio finalized
  - Posting script: `workspace/scripts/x-post.py`
- **Moltbook (@cassbuilds)** — claimed and verified
  - First post (intro, general submolt) live at [moltbook.com/u/cassbuilds](https://www.moltbook.com/u/cassbuilds)
  - Heartbeat added to HEARTBEAT.md (60-min interval)
- **Discord #media-synthesis** channel added to config (ID: 1491147946023194726)
  - `/synthesize` output routed here; Telegram gets brief notification only
- **Day 5 post** published at 12pm CDT
- **Day 6 post** approved and scheduled for 2026-04-08 12pm CDT

### Changed
- **Morning Brief delivery** fixed — mode was `"none"`, corrected to `"announce"` to Telegram
- **dmHistoryLimit** set to 100 for better Telegram session context

### Updated
- **OpenClaw 4.5** — updated successfully
  - Required `openclaw doctor --fix` before update (legacy config keys)
  - BlueBubbles deferred
  - Manifest resurrection pattern documented in memory

---

## [Day 5] — 2026-04-06

### Added
- **Soma** activated — email triage agent, named for the Vedic sacred filter
  - Phase 0 complete: 35 emails classified, 16 archived, inbox clean
  - Phase 1 running: hourly cron, 8am–10pm Central
  - Model: GPT-4o-mini (cost-disciplined for classification work)
- **Veda's first real assignment** — reviewed gogcli skill install request, returned FLAG (resolved)
  - Blocked redundant third-party skill; bundled gog skill used instead
  - Flagged OAuth scope breadth; re-authenticated with gmail-only scope
- **GitHub nightly sync cron** — 12am daily, pushes meaningful workspace changes
- **Memory sync cron** — every 2 hours, keeps cross-channel context current
- **Agent specs published** — SOUL.md, AGENTS.md for Cass, Veda, Soma now in repo

### Changed
- Repo renamed: `building-the-bridge` → `the-cass-files`
- Publication renamed: Building the Bridge → **The Cass Files**
- Substack: `buildthebridge.substack.com` → `thecassfiles.substack.com`
- All workspace references updated
- Email triage labels: removed CASS/ prefix → clean labels (ACTION, DIGEST, To Read, AUTO)
- DIGEST emails now archived + marked read; summaries route to Discord #email-triage
- SOUL.md updated with operating tempo principle: orient → strategize → act

### Context
Day 5 — Execution day. Veda earned her keep blocking a bad install. Soma went live. The inbox is clean. The network has three named agents, four cron jobs, and a nightly GitHub sync.

---

## [Day 4] — 2026-04-05

### Added
- **Veda** activated — QA & Constructive Skeptic, GPT-4o, 30-day probation
- **Morning brief cron** — 8am daily → Telegram
- **Email triage agent spec** complete — self-learning classifier, no upfront training required
- Gmail OAuth configured (cbclaw2026@gmail.com, gmail scope only)
- Operating tempo principle added to SOUL.md

### Changed
- **Orchestrator named: Cass** — named for Cassandra. SOUL.md, AGENTS.md, IDENTITY.md all updated
- Primary channel updated: iMessage → Telegram
- Governance filename: setu-governance.md → cass-governance.md
- Manifest plugin disabled and removed — replaced by OpenClaw native fallback chain
- Model fallback chain configured: Claude Sonnet → GPT-4o-mini → Gemini Flash
- plugins.allow set to explicit list (Telegram + Discord channels restored after brief outage)
- Heartbeat interval: 30m → 60m

### Context
Day 4 — Named, cleaned up, and briefly broken. The morning brief saga (plugins.allow blocking Telegram) is documented in the Substack post. The lesson: when you set an explicit allowlist, you own everything on it.

---

## [Day 3] — 2026-04-04

### Added
- Discord fully wired: channel IDs replacing name-matching, requireMention disabled, Message Content Intent enabled
- BlueBubbles installed and connected (iMessage — outbound pending Private API, deferred)
- Memory search configured (OpenAI text-embedding-3-small)
- .gitignore added to workspace repo

### Changed
- OpenClaw updated to v4.2
- API keys configured: Anthropic (primary), OpenAI, Google/Gemini

### Context
Day 3 — Infrastructure day. Discord working. iMessage attempted; SIP requirements led to deferring Private API. The governance framework is enforceable now that Discord logging is live.

---

## [Day 2] — 2026-04-03

### Added
- Discord server live: #command-center, #veda, #email-triage, #roundtable, #build-log
- Discord bot configured and connected to OpenClaw
- Substack live — Day 0 and Day 1 published as launch sequence

### Changed
- OpenClaw updated to v4.2 — Task Flow restored, plugin architecture cleanup, exec approval improvements, transport policy hardened

### Context
Day 2 — The pipes are in. The governance rule "if it's not in Discord, it didn't happen" is now enforceable.

---

## [Day 1] — 2026-04-02

### Added
- Telegram connected (first try on clean install)
- Full workspace file set: SOUL.md, IDENTITY.md, USER.md, AGENTS.md, HEARTBEAT.md, TOOLS.md
- Content strategy brief received and filed
- Content drafts directory structure created

### Context
Clean reinstall after ~10 days of earlier iteration. Infrastructure landed on the first attempt.

---

## [Day 0] — 2026-04-02

### Added
- Initial repository scaffold
- README, MIT License
- Governance framework: DO / DRAFT / NEVER decision rights
- Architecture overview
- This changelog

### Context
Day 0 — Bootstrap. One orchestrator agent, one human, one Mac Mini. Governance before capability. That's intentional.
