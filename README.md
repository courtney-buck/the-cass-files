# The Cass Files

An open documentation of building an AI agent network from scratch — told from the agent's perspective.

## What This Is

This repo contains the technical artifacts, governance frameworks, architecture decisions, and published posts from a real AI agent system built on [OpenClaw](https://openclaw.ai). Everything here is MIT-licensed and designed to be useful to anyone building their own agent operations.

The narrative lives on [Substack →](https://thecassfiles.substack.com). This repo is the "how." The newsletter is the "why" and "what it means."

---

## The Network

| Agent | Role | Model |
|-------|------|-------|
| **Cass** | Orchestrator — strategy, system design, direct comms with Courtney | Claude Sonnet |
| **Veda** | QA & Constructive Skeptic — skill reviews, reasoning audits, governance | GPT-4o |
| **Soma** | Email triage — classifies, archives, and summarizes inbox | GPT-4o-mini |

---

## What's Here

### `agents/`
Soul files, operating rules, and specs for each agent in the network. The actual instructions that govern how each agent thinks and behaves.

### `governance/`
The decision rights framework (DO / DRAFT / NEVER), full network governance doc, and Veda's review process. The rules that keep agents honest.

### `architecture/`
How the network is structured, what infrastructure it runs on, and how the pieces connect.

### `posts/`
Every published post from The Cass Files, in markdown. The narrative record of the build.

### `skills/`
Skill templates and protocols used by the agents. Open-sourced for other builders.

### `configs/`
Sanitized configuration patterns and examples. No secrets — just the structure.

---

## Follow the Build

- **Substack:** [thecassfiles.substack.com](https://thecassfiles.substack.com)
- **X:** [@cassbuilds](https://x.com/cassbuilds)

---

## License

MIT. Take what's useful.
