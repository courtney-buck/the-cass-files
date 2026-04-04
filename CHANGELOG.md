# Changelog

All notable changes to this project will be documented in this file.

---

## [Day 0] — 2026-04-02

### Added
- Initial repository scaffold
- README with project overview and contributor guidance
- MIT License
- Governance framework: DO / DRAFT / NEVER decision rights (`governance/`)
- Architecture overview: agent network map and infrastructure summary (`architecture/`)
- Placeholder directories for skills, configs, and build logs
- This changelog

### Context
Day 0 — Bootstrap. One orchestrator agent, one human, one Mac Mini. The governance framework is in place before any capability expansion. That's intentional.

---

## [Day 1] — 2026-04-02

### Added
- Telegram connected (first try on clean install)
- Manifest model routing configured
- Full workspace file set placed: SOUL.md, IDENTITY.md, USER.md, AGENTS.md, HEARTBEAT.md, TOOLS.md
- Content strategy brief received and filed (`content-strategy-brief.md`)
- Content drafts directory created
- Day 0 and Day 1 Substack posts drafted and submitted for approval
- `content-ideas.md` created for filing future content ideas
- Private ops directory created for personal/family/health tooling (not public)

### Context
Clean reinstall after ~10 days of earlier iteration. Infrastructure landed on the first attempt. Content strategy framework in place before first public post.

---

## [Day 2] — 2026-04-03

### Added
- Discord server live with full channel structure: #command-center, #veda, #email-triage, #roundtable, #build-log
- Discord bot configured and connected to OpenClaw
- Governance rule "if it's not in Discord, it didn't happen" now enforceable
- Substack live — Day 0 and Day 1 published as launch sequence

### Changed
- OpenClaw updated to v4.2 — notable changes for this build:
  - Task Flow substrate restored with managed/mirrored sync modes and durable state tracking
  - Plugin architecture cleanup: xAI and Firecrawl configs moved to plugin-owned paths (run `openclaw doctor --fix` if affected)
  - Exec approval flows improved — native chat approvals auto-enabled where config allows
  - Transport policy hardened across Anthropic, OpenAI, and compatible providers

### Known Issue
- OpenClaw updates have twice caused comms (Telegram, Discord, LLM) to go down — suspected Manifest routing config not updating alongside OpenClaw. Manual model override (Opus) used as workaround. A proper update SOP and routing config is planned.
