# OpenClaw Configuration Patterns

Sanitized patterns from a real production setup. Values are placeholders — structure is real.

These represent lessons learned, not Day 0 defaults. Each pattern has a "why it matters" note.

---

## Model Fallback Chain

```json5
{
  agents: {
    defaults: {
      model: {
        primary: "anthropic/claude-sonnet-4-6",
        fallbacks: [
          "openai/gpt-4o-mini",
          "google/gemini-2.0-flash"
        ]
      }
    }
  }
}
```

**Why it matters:** When Anthropic rate-limits (it happens), the system routes automatically instead of going silent. gpt-4o-mini is fast and cheap as a fallback; gemini-flash is the free-tier safety net.

---

## plugins.allow — Always Set Explicitly

```json5
{
  plugins: {
    allow: [
      "telegram",
      "discord",
      "bluebubbles",
      "anthropic",
      "openai",
      "google",
      "brave",
      "memory-core"
    ]
  }
}
```

**Why it matters:** If you leave `plugins.allow` empty, OpenClaw warns but loads everything. If you set it to a partial list (e.g., just `["bluebubbles"]`), Telegram and Discord silently fail to load — no error, just no channel. When you set an explicit allowlist, you own every entry on it.

---

## Telegram — Proactive Outbound (defaultTo)

```json5
{
  channels: {
    telegram: {
      enabled: true,
      dmPolicy: "allowlist",
      allowFrom: ["YOUR_TELEGRAM_USER_ID"],
      defaultTo: "YOUR_TELEGRAM_USER_ID",  // Must be a string, not integer
      groupPolicy: "allowlist"
    }
  }
}
```

**Why it matters:** `defaultTo` enables proactive outbound messages (cron jobs, alerts) without an active session. Must be a string — storing as integer silently breaks channel initialization.

---

## Discord — Guild + Channel Allowlist (Stable IDs)

```json5
{
  channels: {
    discord: {
      enabled: true,
      groupPolicy: "allowlist",
      dmPolicy: "allowlist",
      allowFrom: ["YOUR_DISCORD_USER_ID"],
      guilds: {
        "YOUR_SERVER_ID": {
          requireMention: false,   // false for private servers
          users: ["YOUR_DISCORD_USER_ID"],
          channels: {
            "CHANNEL_ID_1": { enabled: true },
            "CHANNEL_ID_2": { enabled: true }
          }
        }
      }
    }
  }
}
```

**Why it matters:** Use stable numeric IDs, not channel names. Name-matching is disabled by default — `#command-center` in allowFrom does nothing without `dangerouslyAllowNameMatching: true`. Get IDs from Discord Developer Mode (right-click → Copy ID).

---

## Memory Search — OpenAI Embeddings

```json5
{
  agents: {
    defaults: {
      memorySearch: {
        provider: "openai",
        model: "text-embedding-3-small"
      }
    }
  }
}
```

**Why it matters:** Semantic memory recall needs an embedding provider. `text-embedding-3-small` is ~$0.02/1M tokens — effectively free for personal use.

---

## Cron — Morning Brief to Telegram

```json5
// openclaw cron add equivalent
{
  name: "morning-brief",
  schedule: { kind: "cron", expr: "0 8 * * *", tz: "America/Chicago" },
  sessionTarget: "session:agent:main:telegram:direct:YOUR_TELEGRAM_USER_ID",
  payload: {
    kind: "agentTurn",
    message: "Deliver morning brief to Courtney...",
    model: "anthropic/claude-sonnet-4-6",
    timeoutSeconds: 120
  },
  delivery: {
    mode: "announce",
    channel: "telegram",
    to: "YOUR_TELEGRAM_USER_ID"
  }
}
```

**Why it matters:** Binding to the existing Telegram session key (not isolated) ensures the reply routes correctly to your DM. `announce` mode + explicit `to` is required for proactive Telegram delivery.

---

## dmHistoryLimit — Telegram Context Window

```json5
{
  channels: {
    telegram: {
      dmHistoryLimit: 100
    }
  }
}
```

**Why it matters:** The default Telegram DM history is low — the agent loses context for longer conversations or multi-step tasks. Setting `dmHistoryLimit: 100` keeps enough message history that cron-driven briefs can reference recent conversation without confusion.

---

## Channel-Specific Output Routing (Discord)

For agents or scripts that need to route specific output types to dedicated Discord channels:

```json5
// In openclaw.json
{
  channels: {
    discord: {
      guilds: {
        "YOUR_SERVER_ID": {
          channels: {
            "MEDIA_SYNTHESIS_CHANNEL_ID": { enabled: true }  // e.g., #media-synthesis
          }
        }
      }
    }
  }
}
```

Then in the script/cron, send to that channel explicitly and send a brief summary to Telegram:

```python
# Route full output to Discord
message_discord(channel_id=MEDIA_SYNTHESIS_CHANNEL_ID, content=full_output)
# Brief to Telegram
message_telegram(to=USER_ID, content=f"Synthesis complete: {title}")
```

**Why it matters:** Telegram gets noisy fast with long-form content. Routing rich output (transcripts, syntheses) to a dedicated Discord channel keeps Telegram clean for decisions and alerts.

---

## Update SOP

When running `openclaw update`:

1. `openclaw doctor --fix` first (clears legacy config keys)
2. `openclaw update`
3. Check `ls ~/.openclaw/extensions/` — third-party extensions can resurrect after doctor --fix
4. If unwanted extensions reappear: `rm -rf ~/.openclaw/extensions/<name>`
5. `openclaw gateway restart`
6. `openclaw channels status --probe` — verify all channels back up before done

---

*Updated: Day 6 — 2026-04-06*
