# OpenClaw Workspace Configuration Plan

## Status: Research Complete

---

## What OpenClaw Is

OpenClaw was created by **Peter Steinberger** (steipete, peter@openclaw.ai), founder of PSPDFKit.
Website: https://openclaw.ai. Formerly known as Clawdbot, then Moltbot.
Featured in MacStories by Federico Viticci: "OpenClaw Showed Me What the Future of Personal AI Assistants Looks Like."

Kris (kristofmuys) runs his own instance using forked repos.

**Upstream repos:**
- `openclaw/openclaw` - the OpenClaw platform
- `VoltAgent/awesome-openclaw-skills` - community skills catalog
- `hesamsheikh/awesome-openclaw-usecases` - community use cases

**Kris's forks:**
- `kristofmuys/openclaw`
- `kristofmuys/awesome-openclaw-skills`
- `kristofmuys/awesome-openclaw-usecases`
- `kristofmuys/OpenClaw_md` - this workspace

**Install:**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
```

**Model aliases (from src/config/defaults.ts):**
- `sonnet` = `anthropic/claude-sonnet-4-6`
- `opus` = `anthropic/claude-opus-4-6`

**Config format (openclaw.json, json5):**
```json5
{
  agent: {
    model: "anthropic/claude-sonnet-4-6",
  },
}
```

---

## Official Template vs This Workspace

Researched from `openclaw/openclaw/docs/reference/templates/`.

### AGENTS.md
**Official template covers:**
- First run ritual (read BOOTSTRAP.md)
- Every session: read SOUL.md, USER.md, memory files
- Memory system (daily notes + MEMORY.md)
- Safety rules
- External vs internal actions
- Group chat behavior (when to speak, when to stay silent)
- Emoji reactions
- Voice storytelling (if sag/ElevenLabs available)
- Platform formatting (Discord/WhatsApp: no markdown tables)
- Heartbeat guidance (HEARTBEAT_OK, when to reach out)
- Cron vs heartbeat decision guide
- Memory maintenance during heartbeats

**This workspace's AGENTS.md:**
- Has security rules, data classification, writing style, message pattern, cron standards, subagent policy, model strategy, error reporting, group chat protocol, heartbeat
- Missing: group chat reaction guidance, voice storytelling, platform formatting rules, heartbeat proactivity guidance, cron vs heartbeat decision guide

### TOOLS.md
**Official template:** Camera names, SSH hosts, TTS voices, device nicknames - environment-specific setup notes.

**This workspace's TOOLS.md:** Has Telegram topic IDs, model config, gateway port, paths, API token locations, voice memo rules, content preferences. This is a valid customization for Kris's setup.

### HEARTBEAT.md
**Official template:** Essentially empty ("Keep this file empty to skip heartbeat API calls. Add tasks below when you want the agent to check something periodically.")

**This workspace's HEARTBEAT.md:** Has a detailed checklist. This is a valid customization.

### BOOTSTRAP.md
**Official template:** Conversational first-run ritual - figure out name, nature, vibe, emoji together. Then update IDENTITY.md and USER.md. Then optionally connect channels.

**This workspace's BOOTSTRAP.md:** Has a structured setup checklist with specific commands. Different approach but valid.

### SOUL.md, IDENTITY.md, USER.md
These are all valid customizations of the official templates.

---

## Corrections Applied (Committed to main)

1. **Model**: `claude-sonnet-4-5` → `anthropic/claude-sonnet-4-6` (all files)
2. **Creator**: Removed false claim Kris maintains OpenClaw. Peter Steinberger created it.
3. **Upstream repos**: Added correct upstream references
4. **Telegram topics**: Expanded from 5 to 11 (matching prompt 11)
5. **USER.md**: Removed false claim Kris maintains OpenClaw
6. **README.md**: Correct install command, correct creator, correct upstream repos
7. **SUBAGENT-POLICY.md**: Model references updated
8. **docs/WORKSPACE-FILES.md**: Header updated

---

## Remaining Placeholders

| File | Field | Current Value |
|------|-------|---------------|
| `USER.md` | Work email | `kris@example.com` |
| `TOOLS.md` | Telegram Group ID | `*(set after Telegram group is created)*` |
| `TOOLS.md` | All 11 topic thread IDs | `*(set after topic creation)*` |
| `MEMORY.md` | Personal email | `*(add when known)*` |

---

## Potential Further Improvements (Not Yet Done)

These are observations from comparing with official templates. Not making changes without direction.

1. **AGENTS.md**: Missing group chat reaction guidance, voice storytelling, platform formatting rules (Discord/WhatsApp no markdown tables), heartbeat proactivity guidance, cron vs heartbeat decision guide. The official template has much richer guidance.

2. **SUBAGENT-POLICY.md**: This file doesn't exist in the official templates. OpenClaw handles subagents natively. This file may be unnecessary or could be merged into AGENTS.md.

3. **docs/WORKSPACE-FILES.md**: This is a custom doc not in the official templates. It's useful but adds token cost.

4. **BOOTSTRAP.md**: Should be deleted after first session completes (per its own instructions).
