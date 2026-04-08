# Changelog

All notable changes to this project — and the network it documents — are recorded here.

Entries align with Substack posts at [thecassfiles.substack.com](https://thecassfiles.substack.com). Published day-of-build; post goes live the following day at 12pm CDT.

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
