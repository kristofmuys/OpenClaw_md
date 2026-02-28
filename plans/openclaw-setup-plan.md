# OpenClaw Workspace Configuration Plan

## Status: Research Complete

---

## What OpenClaw Is

OpenClaw was created by **Peter Steinberger** (steipete, peter@openclaw.ai), founder of PSPDFKit.
Website: https://openclaw.ai. Full name history: **Warelay -> Clawdbot -> Moltbot -> OpenClaw**.
Featured in MacStories by Federico Viticci: "OpenClaw Showed Me What the Future of Personal AI Assistants Looks Like."
Current version: 2026.2.27 (date-based versioning). Very active project with many contributors.

**Security context (from trust.openclaw.ai):** OpenClaw has documented cases of malicious actors attempting
to exploit AI agent platforms (prompt injection, indirect injection, tool abuse, identity risks).
This is why the workspace AGENTS.md has extensive security rules - they're based on real documented attacks.
OpenClaw partnered with VirusTotal to scan skills on ClawHub (the skill marketplace).
Security program: trust.openclaw.ai. Security audit: `openclaw security audit --deep`.

**OpenClaw security defaults:**
- DM Policy: Pairing (unknown senders must complete pairing flow with expiring code)
- Exec Security: Deny with ask on-miss (dangerous commands require approval)
- AllowFrom: Self-only by default
- Session Isolation: Conversations isolated per session key
- SSRF Protection: Internal IPs and localhost blocked in web_fetch
- Gateway Auth: Required by default

**MacStories article key facts:**
- Federico Viticci used Claude Opus 4.5 (not Sonnet) for his setup
- He named his agent "Navi" (users name their own agents)
- OpenClaw runs on M4 Mac mini (local machine)
- Skills can be created on-the-fly by the agent itself
- The agent can build things autonomously overnight ("proactive work")

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

## Critical Findings from Source Code Research

### 1. MEMORY.md Loading Behavior (INCORRECT in workspace docs)

From `src/agents/workspace.ts` (`filterBootstrapFilesForSession`):

**Actual behavior:**
- Main sessions (direct chat, group chat): ALL files loaded including MEMORY.md
- Subagent sessions: Only AGENTS.md, TOOLS.md, SOUL.md, IDENTITY.md, USER.md
- Cron sessions: Only AGENTS.md, TOOLS.md, SOUL.md, IDENTITY.md, USER.md

**What workspace docs claim:**
- `docs/WORKSPACE-FILES.md`: "Direct chats with Kris only. Excluded from group/shared contexts"
- `AGENTS.md`: "Only load in direct/private chats"
- `MEMORY.md`: "Only loaded in private/direct chats with Kris. Never in group contexts."

**The truth:** MEMORY.md is loaded in ALL main sessions, including group chats. The "private chat only" behavior is NOT enforced by OpenClaw's code. It's just an instruction to the agent. The agent must follow this instruction itself.

This means the MEMORY.md privacy claim is aspirational, not technical. The agent is instructed to not reference MEMORY.md in group contexts, but the file IS loaded.

### 2. SUBAGENT-POLICY.md is Not a Standard OpenClaw File

OpenClaw does not load SUBAGENT-POLICY.md. It's not in the workspace file constants. The workspace AGENTS.md references it ("See SUBAGENT-POLICY.md for the full policy") but OpenClaw won't load it automatically.

If this file is needed, its content should be merged into AGENTS.md, or it should be added to the `agents.bootstrap.extra` config to be loaded explicitly.

### 3. docs/WORKSPACE-FILES.md is Not Loaded by OpenClaw

This file is not in the workspace file constants. It's documentation for humans, not for the agent. It does NOT get loaded into the system prompt.

### 4. File Loading Order (from source)

Main sessions load in this order:
1. AGENTS.md
2. SOUL.md
3. TOOLS.md
4. IDENTITY.md
5. USER.md
6. HEARTBEAT.md
7. BOOTSTRAP.md (if exists)
8. MEMORY.md (if exists)

---

## Potential Further Improvements (Not Yet Done)

These are observations from comparing with official templates. Not making changes without direction.

1. **AGENTS.md**: Missing group chat reaction guidance, voice storytelling, platform formatting rules (Discord/WhatsApp no markdown tables), heartbeat proactivity guidance, cron vs heartbeat decision guide. The official template has much richer guidance.

2. **SUBAGENT-POLICY.md**: Not loaded by OpenClaw. Content should be in AGENTS.md or added to `agents.bootstrap.extra` config.

3. **docs/WORKSPACE-FILES.md**: Not loaded by OpenClaw. Documentation only.

4. **BOOTSTRAP.md**: Should be deleted after first session completes (per its own instructions).

5. **MEMORY.md privacy claim**: The "private chat only" claim is aspirational, not technical. The agent must enforce this itself via its instructions.
