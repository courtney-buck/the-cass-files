# AGENT-STATE.md
# Current system state. Read this before acting in any isolated or low-context session.
# Updated by memory-sync every 2 hours. Last updated: 2026-04-10 09:00 CDT

---

## OpenClaw Version
- **Installed:** v4.9
- **Manifest:** Installed clean (one instance). Model routing active via Manifest dashboard (http://127.0.0.1:2099).

---

## Model Assignments
| Job | Model | Rationale |
|-----|-------|-----------|
| morning-brief | claude-sonnet-4-6 | Strategic, needs reasoning |
| evening-recap | claude-sonnet-4-6 | Strategic, reads memory |
| memory-sync | claude-haiku-4-5 | Read/compare/append — no reasoning needed |
| moltbook-heartbeat | claude-haiku-4-5 | Single API call + summarize |
| github-push | claude-sonnet-4-6 | Judgment on what to commit |
| media-discovery | claude-sonnet-4-6 | Quality filtering requires judgment |
| soma-triage | openai/gpt-4o-mini | Email classification, cost-sensitive |
| publish-reminders | claude-haiku-4-5 | Simple file move + notification |

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
| moltbook-heartbeat | Hourly (staggered) | haiku | ✅ Running |
| github-push | Midnight CDT | sonnet | ✅ Running |
| media-discovery | 7am CDT daily | sonnet | ✅ Running |
| soma-triage | Hourly 8am–10pm CDT | gpt-4o-mini | ⚠️ MISSING — cron job not found in job list as of Apr 10. Needs re-creation or investigation |
| x-post-3 | Apr 10 10am CDT | sonnet | ⏳ Scheduled |
| x-post-4 | Apr 11 10am CDT | sonnet | ⏳ Scheduled |
| x-post-5 | Apr 12 10am CDT | sonnet | ⏳ Scheduled |
| day8-publish-reminder | Apr 10 12pm CDT | haiku | ⏳ Scheduled |

---

## Content Pipeline
| Post | Status | Scheduled |
|------|--------|-----------|
| Day 1–7 | Published ✅ | — |
| Day 8 | Approved, in drafts | Apr 10, 12pm CDT |
| Day 9+ | Not started | — |

**X post queue:** Apr 10–12 at 10am CDT. Queue needs replenishment after Apr 12.

---

## Open Decisions / Pending
- courtneyfbuck@gmail.com inbox: 5,223 emails. Dry run cancelled. Classification rules to be determined via Claude/ChatGPT membership session (flat-rate, not per-token). Soma re-enable pending that review.
- Soma personal Gmail: paused until Courtney completes retroactive rule-building
- Substack custom domain / setup: awaiting response from Substack support
- Elevated agent: architecture session needed before any build
- Agent registry: identified as Phase 1 infrastructure, not yet built
- Weekly calibration Sunday Telegram message: not yet wired up
- SQLite audit log for Soma: deferred

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
- **Soma triage cron missing** — not present in cron job list as of Apr 10 09:00. Was listed in AGENT-STATE.md as active. May need re-creation.
- Soma triage was timing out at 120s on cbclaw2026 — monitor next run
- Manifest had been running 3-4x prior to Apr 9 reinstall — root cause: multiple installs accumulated. Now clean.
- Publish reminder crons previously used `cp` (left drafts behind). Now corrected to `mv`.
