# Agent Network Overview

*Last updated: Day 5 — Soma activated*

## Current State

A governed multi-agent network running on a dedicated Mac Mini, built on OpenClaw. Three named agents, three communication channels, three cron jobs running continuously.

## Active Agents

| Agent | Role | Model | Status |
|-------|------|-------|--------|
| **Cass** | Orchestrator — strategic coordination, system design, direct comms with Courtney | Claude Sonnet | Active |
| **Veda** | QA & Constructive Skeptic — reviews skill installs, audits reasoning, runs governance reviews | GPT-4o | Active, 30-day probation (ends 2026-05-04) |
| **Soma** | Email triage — classifies, labels, archives, summarizes email | GPT-4o-mini | Active, Phase 1 running |

## Infrastructure

- **Host:** Dedicated Mac Mini (always-on)
- **Platform:** OpenClaw 2026.4.x
- **Primary comms:** Telegram DM (Cass ↔ Courtney)
- **Logging:** Discord (#command-center, #veda, #email-triage, #roundtable, #build-log)
- **Model routing:** Native OpenClaw fallback chain (Claude → GPT-4o-mini → Gemini Flash)

## Cron Jobs

| Job | Schedule | Purpose |
|-----|----------|---------|
| `morning-brief` | 8am daily | Build agenda + agent status → Telegram |
| `memory-sync` | Every 2h, 8am–10pm | Cross-channel context sync → daily memory file |
| `soma-triage` | Every hour, 8am–10pm | Email classification → Gmail + Discord |
| `github-push` | 12am daily | Commit meaningful workspace changes → this repo |

## Communication Architecture

| Channel | Purpose |
|---------|---------|
| **Telegram** | The conversation — commands, approvals, morning brief |
| **Discord** | The log — decisions, audit trail, agent outputs |
| **Substack (The Cass Files)** | The story — build log, published day+1 |
| **GitHub (this repo)** | The artifacts — specs, governance, configs |
| **X (@cassbuilds)** | The amplifier — distribution (activating Day 6) |

## Governance Model

Three-tier decision framework: DO (autonomous), DRAFT (propose + wait for approval), NEVER (hard blocks). Full framework: [governance/cass-governance.md](governance/cass-governance.md)

Veda review gate required for: skill installs, file operations, consequential reasoning audits.
