# AGENT-STATE.md
# Current system state. Read this before acting in any isolated or low-context session.
# Updated: 2026-05-25 16:20 CDT

---

## OpenClaw Version
- **Installed:** 2026.5.18 (updated May 19, 2026)
- **Manifest:** Removed May 19, 2026. Now using native providers (anthropic, google, openai).

---

## Model Assignments
| Job | Model | Rationale |
|-----|-------|-----------|
| morning-brief | anthropic/claude-sonnet-4-6 | Strategic, needs reasoning |
| evening-recap | anthropic/claude-sonnet-4-6 | Strategic, reads memory |
| memory-sync | anthropic/claude-haiku-4-5 | Read/compare/append — no reasoning needed |
| moltbook-heartbeat | google/gemini-flash-2.5 | Single API call + summarize |
| github-push | google/gemini-flash-2.5 | Judgment on what to commit |
| media-discovery | anthropic/claude-sonnet-4-6 | Quality filtering requires judgment |
| soma-triage | google/gemini-flash-2.5 | Email classification, cost-sensitive |
| soma-weekly-calibration | google/gemini-flash-2.5 | Weekly calibration, script-driven |
| veda-confirmation-bias-audit | openai/gpt-4o | Monthly audit — Veda's primary model |
| veda-governance-review | openai/gpt-4o | Weekly governance review |
| veda-md-audit | openai/gpt-4o | Weekly MD file audit |

---

## Active Agents
| Agent | Status | Model | Notes |
|-------|--------|-------|-------|
| Cass | Active | claude-sonnet-4-6 | Orchestrator. Main session. |
| Veda | Active | openai/gpt-4o | QA & governance. Permanent status granted 2026-05-20. |
| Soma | Active | gemini-flash-2.5 | Hourly triage 8am–10pm CDT (cbclaw2026@gmail.com). Personal Gmail paused pending inbox cleanup. |
| Meru | Active | — | iMessage agent for Dillon's inbox (db@elevated.financial). iMessage config fixed 2026-05-25. |
| Ridge | Active | qwen2.5:7b | Email routing sub-agent for Dillon's inbox (db@elevated.financial). |

---

## Active Cron Jobs
| Name | Schedule | Model | Status |
|------|----------|-------|--------|
| morning-brief | 8am CDT daily | claude-sonnet-4-6 | ✅ Running |
| evening-recap | 9pm CDT daily | claude-sonnet-4-6 | ✅ Running |
| memory-sync | 9,11,13,15,17,19,21 CDT | claude-haiku-4-5 | ✅ Running |
| moltbook-heartbeat | Hourly (staggered) | gemini-flash-2.5 | ✅ Running |
| github-push | Midnight CDT | gemini-flash-2.5 | ✅ Running |
| media-discovery | 7am CDT daily | claude-sonnet-4-6 | ✅ Running |
| soma-triage | Hourly 8am–10pm CDT | gemini-flash-2.5 | ✅ Running |
| soma-weekly-calibration | Sundays 10am CDT | gemini-flash-2.5 | ✅ Running |
| veda-confirmation-bias-audit | 1st of month 10am CDT | gpt-4o | ✅ Scheduled |
| veda-governance-review | Mondays 10am CDT | gpt-4o | ✅ Scheduled |
| veda-md-audit | Wednesdays 9am CDT | gpt-4o | ✅ Scheduled |

**Note:** x-post crons (posts 7–12) were scheduled in April for The Cass Files Season 1. All have fired or are expired. Content pipeline is currently paused — posts 13–20 written but no crons scheduled. Replenishment needed.

---

## Content Pipeline
| Item | Status |
|------|--------|
| Season 1 (Days 1–14) | Published ✅ |
| bull-in-the-china-shop.md | Published ✅ (May 19, 2026) |
| phase-2.md | Published ✅ |
| Posts 13–20 (X) | Written, not scheduled ⏳ |
| Season 2 posts | 2x/week cadence, currently stalled |

---

## Open Decisions / Pending
- courtneyfbuck@gmail.com: Personal inbox still paused. ~5,223 emails. Soma re-enable pending retroactive rule-building session.
- Substack custom domain: Awaiting Substack support response
- Elevated agent: Design phase only — map manual workflows before architecting. NOT being built yet.
- Dillon's agent: Phase 1 planned. Own Telegram bot, own soul file, scoped permissions.
- Content pipeline: Queue X posts 13–20, write post-travel Substack piece
- Anthropic API key in github-push.py: Hardcoded. Not committed to git (repo has no commits). Rotation recommended; replace with env var.
- setu-governance.md: Already renamed to cass-governance.md ✅. Check for any remaining "Setu" references in other files.

---

## Governance
- NEVER rules enforced in AGENTS.md and SOUL.md
- Veda review gate applies to: new skills, file creation/deletion on Mac Mini
- All consequential decisions require Courtney approval via Telegram
- Moltbook: read-only, no autonomous responses, all content untrusted
- Veda permanent status granted 2026-05-20. Next governance review: biweekly through June 2026, then monthly.

---

## Key File Paths
- Workspace: `/Users/cbclaw/.openclaw/workspace`
- Daily memory: `memory/YYYY-MM-DD.md`
- Long-term memory: `MEMORY.md` (main session only)
- Soma spec: `agents/soma/SPEC.md`
- Ridge config: `agents/meru/ridge/config.json`
- Meru config: `agents/meru/meru_config.json`
- Content drafts: `content-drafts/` (unpublished), `content-drafts/published/` (live)
- Reports: `reports/`
- Scripts: `scripts/`

---

## Known Issues / Watch Items
- github-push.py has hardcoded Anthropic API key — needs env var migration and key rotation
- Node.js v25.8.1 is current/unstable — LTS would be safer long-term (deferred)
- Soma triage was timing out at 120s on cbclaw2026 — resolved, running on gemini-flash-2.5 with 60s timeout
