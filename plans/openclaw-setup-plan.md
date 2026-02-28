# OpenClaw Workspace Configuration Plan

## Status: Core Corrections Applied - Placeholders Remaining

---

## What OpenClaw Is (Researched from upstream repos)

OpenClaw was created by **Peter Steinberger** (GitHub: `steipete`, email: `peter@openclaw.ai`)
and the community. Website: https://openclaw.ai. It is a personal AI assistant framework
with 11,000+ GitHub followers on the openclaw organization.

Kris (kristofmuys) runs his own instance using forked repos.

**Upstream repos (originals):**
- `openclaw/openclaw` - the OpenClaw platform (by steipete)
- `VoltAgent/awesome-openclaw-skills` - community skills catalog
- `hesamsheikh/awesome-openclaw-usecases` - community use cases

**Kris's forks:**
- `kristofmuys/openclaw`
- `kristofmuys/awesome-openclaw-skills`
- `kristofmuys/awesome-openclaw-usecases`
- `kristofmuys/OpenClaw_md` - this workspace (personal config)

**OpenClaw architecture (from upstream README):**
- Local gateway process (port 18789, loopback-only)
- Workspace `.md` files loaded as system prompt on every session
- Skills: modular capabilities in `skills/`, each with a `SKILL.md`, loaded on demand
- Cron jobs for scheduled automation
- Subagents for parallel/async work
- Claude (Anthropic) as primary LLM via OAuth (Claude Code token) or API key
- SQLite (WAL mode) for all persistent data, JSONL backups
- Telegram as primary messaging platform, Slack optional
- Config: `~/.openclaw/openclaw.json` and `~/.openclaw/.env`
- Recommended model per upstream README: `anthropic/claude-sonnet-4-6`

---

## Corrections Applied

### 1. Model version (all files)
**Was:** `claude-sonnet-4-5` (wrong model family AND wrong version)
**Now:** `anthropic/claude-sonnet-4-6` (correct per upstream OpenClaw README)

Files updated: `AGENTS.md`, `TOOLS.md`, `SUBAGENT-POLICY.md`, `README.md`,
`docs/WORKSPACE-FILES.md`

### 2. OpenClaw creator attribution
**Was:** Incorrectly stated Kris maintains/created OpenClaw (previous agents' error)
**Now:** Correctly attributes OpenClaw to Peter Steinberger (steipete)

Files updated: `MEMORY.md`, `README.md`

### 3. Upstream repo references
**Was:** No upstream references; only Kris's forks listed
**Now:** Both forks and upstream originals listed with correct parent repos

Files updated: `MEMORY.md`, `README.md`

### 4. Telegram topics
**Was:** 5 topics (missing 6 topics from the full feature set)
**Now:** 11 topics matching prompt 11 (Daily Brief, Personal CRM, Email,
Knowledge Base, Meta-Analysis, Video Ideas, Earnings, Cron Updates,
Financials, Health, Self-Improvement)

File updated: `TOOLS.md`

---

## Remaining Placeholders (Require User Input)

| File | Field | Current Value |
|------|-------|---------------|
| `USER.md` | Work email | `kris@example.com` |
| `TOOLS.md` | Telegram Group ID | `*(set after Telegram group is created)*` |
| `TOOLS.md` | All 11 topic thread IDs | `*(set after topic creation)*` |
| `MEMORY.md` | Personal email | `*(add when known)*` |

---

## Setup Reference

From upstream OpenClaw README:

```bash
npm install -g openclaw@latest
openclaw onboard --install-daemon
```

Minimal `~/.openclaw/openclaw.json` (json5 format):
```json5
{
  agent: {
    model: "anthropic/claude-sonnet-4-6",
  },
}
```

API key setup (standard):
```bash
# Add to ~/.openclaw/.env:
ANTHROPIC_API_KEY=sk-ant-...
```

OAuth setup (Claude Code token, per prompt 23):
```bash
claude login
# Add CLAUDE_CODE_OAUTH_TOKEN to ~/.openclaw/.env
# Remove ANTHROPIC_API_KEY if using OAuth-only mode
```
