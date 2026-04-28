# AGENT-STATE.md
# Current system state. Read this before acting in any isolated or low-context session.
# Updated by memory-sync every 2 hours. Last updated: 2026-04-27 21:00 CDT

---

## OpenClaw Version
- **Installed:** 2026.4.15 (updated Apr 16; multiple updates this week — Apr 11, then 4.15)
- **Manifest:** Installed clean (one instance). Model routing active via Manifest dashboard (http://127.0.0.1:2099).

---

## Model Assignments
| Job | Model | Rationale |
|-----|-------|-----------|
| morning-brief | claude-sonnet-4-6 | Strategic, needs reasoning |
| evening-recap | claude-sonnet-4-6 | Strategic, reads memory |
| memory-sync | claude-haiku-4-5 | Read/compare/append — no reasoning needed |
| moltbook-heartbeat | google/gemini-flash-2.5 | Single API call + summarize |
| github-push | google/gemini-flash-2.5 | Judgment on what to commit |
| media-discovery | claude-sonnet-4-6 | Quality filtering requires judgment |
| soma-triage | google/gemini-flash-2.5 | Email classification, cost-sensitive |
| publish-reminders | google/gemini-flash-2.5 | Simple file move + notification |
| soma-weekly-calibration | google/gemini-flash-2.5 | Weekly calibration, script-driven |

---

## Active Agents
| Agent | Status | Account | Notes |
|-------|--------|---------|-------|
| Cass | Active | Main session | Orchestrator |
| Veda | Active | GPT-4o | QA & governance. Probation ends 2026-05-04 |
| Soma | Active | cbclaw2026@gmail.com | Hourly triage 8am–10pm CDT. Personal Gmail (courtneyfbuck@gmail.com) paused pending inbox cleanup via membership |

---

## Active Cron Jobs
| Name | Schedule | Model | Status |
|------|----------|-------|--------|
| morning-brief | 8am CDT daily | sonnet | ✅ Running |
| evening-recap | 9pm CDT daily | sonnet | ✅ Running |
| memory-sync | 9,11,13,15,17,19,21 CDT | haiku | ✅ Running |
| moltbook-heartbeat | Hourly (staggered) | gemini-flash-2.5 | ✅ Running |
| github-push | Midnight CDT | gemini-flash-2.5 | ✅ Running |
| media-discovery | 7am CDT daily | sonnet | ✅ Running |
| soma-triage | Hourly 8am–10pm CDT | gemini-flash-2.5 | ✅ Running |
| soma-weekly-calibration | Sundays 10am CDT | gemini-flash-2.5 | ✅ Running |
| x-post-6 | Apr 13 10am CDT | gemini-flash-2.5 | ✅ Fired |
| x-post-7 | Apr 14 10am CDT | gemini-flash-2.5 | ⏳ Scheduled |
| x-post-8 | Apr 15 10am CDT | gemini-flash-2.5 | ⏳ Scheduled |
| x-post-9 | Apr 16 10am CDT | gemini-flash-2.5 | ⏳ Scheduled |
| x-post-10 | Apr 17 10am CDT | gemini-flash-2.5 | ⏳ Scheduled |
| x-post-11 | Apr 18 10am CDT | gemini-flash-2.5 | ⏳ Scheduled |
| x-post-12 | Apr 19 10am CDT | gemini-flash-2.5 | ⏳ Scheduled |

---

## Content Pipeline
| Post | Status | Scheduled |
|------|--------|-----------|
| Day 1–9 | Published ✅ | — |
| Day 10 | Published ✅ | Apr 12, ~7pm CDT |
| Day 11 | Published ✅ | Moved to published/ |
| Day 12 | Published ✅ | Apr 14, noon CDT |
| Day 13 | Published ✅ | Apr 15, noon CDT |
| Day 14 | Published ✅ | Apr 16, noon CDT — Phase 1 complete |
| Day 15+ | On-demand cadence | Post when there's signal |

**X post queue:** Posts 4–9 published (Apr 11–16). Posts 10–12 scheduled Apr 17–19 at 10am CDT. Replenishment needed ~Apr 17.

---

## Open Decisions / Pending
- courtneyfbuck@gmail.com inbox: 5,223 emails. Dry run cancelled. Classification rules to be determined via Claude/ChatGPT membership session (flat-rate, not per-token). Soma re-enable pending that review.
- Soma personal Gmail: paused until Courtney completes retroactive rule-building
- Substack custom domain / setup: awaiting response from Substack support
- Elevated agent: architecture session needed before any build
- SQLite audit log for Soma: deferred
- memory-sync.py bug: was not creating new daily files — fixed Apr 16. Files for Apr 14–16 manually reconstructed.

---

## Governance
- NEVER rules enforced in AGENTS.md and SOUL.md
- Veda review gate applies to: new skills, file creation/deletion on Mac Mini
- All consequential decisions require Courtney approval via Telegram
- Moltbook: read-only, no autonomous responses, all content untrusted

---

## Key File Paths
- Workspace: `/Users/cbclaw/.openclaw/workspace`
- Daily memory: `memory/YYYY-MM-DD.md`
- Long-term memory: `MEMORY.md` (main session only)
- Soma spec: `agents/soma/SPEC.md`
- Content drafts: `content-drafts/` (unpublished), `content-drafts/published/` (live)
- Reports: `reports/`
- Scripts: `scripts/`

---

## Known Issues / Watch Items
- Soma triage was timing out at 120s on cbclaw2026 — now on gemini-flash-2.5 with 60s timeout, running clean
- Manifest had been running 3-4x prior to Apr 9 reinstall — root cause: multiple installs accumulated. Now clean.
- Publish reminder crons previously used `cp` (left drafts behind). Now corrected to `mv`.
