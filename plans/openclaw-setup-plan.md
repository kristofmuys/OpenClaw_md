# OpenClaw Workspace Configuration Plan

## Status: Research Complete - Ready for Corrections

---

## What OpenClaw Is (Researched)

OpenClaw was created by **Matt Berman** (GitHub: `mberman84`, YouTube: Matt Berman AI).
Matt Berman is a prominent AI content creator and tech commentator who built OpenClaw
as his personal AI assistant framework. It has been covered extensively in AI/tech news.

Kris (kristofmuys) is a user of OpenClaw who forked the repos to run his own instance.
The repos in this workspace (`kristofmuys/openclaw`, etc.) are forks of Matt Berman's
original repos (`mberman84/openclaw`, `mberman84/awesome-openclaw-skills`,
`mberman84/awesome-openclaw-usecases`).

**OpenClaw architecture:**
- Local gateway process (port 18789, loopback-only)
- Workspace `.md` files loaded as system prompt on every session
- Skills: modular capabilities in `skills/`, each with a `SKILL.md`, loaded on demand
- Cron jobs for scheduled automation
- Subagents for parallel/async work
- Claude (Anthropic) as primary LLM via OAuth (Claude Code token) or API key
- SQLite (WAL mode) for all persistent data, JSONL backups
- Telegram as primary messaging platform, Slack optional
- Config: `~/.openclaw/openclaw.json` and `~/.openclaw/.env`

---

## Errors Introduced by Previous Agents

### 1. MEMORY.md: False Claim About Kris's Role

**Current (wrong):**
```
Kris maintains the OpenClaw project and related community repos:
- `kristofmuys/openclaw` - the main OpenClaw platform
- `kristofmuys/awesome-openclaw-skills` - community skills catalog
- `kristofmuys/awesome-openclaw-usecases` - community use cases
- `kristofmuys/OpenClaw_md` - this workspace (personal OpenClaw config)
```

**Should be:**
Kris uses OpenClaw (created by Matt Berman / mberman84). His repos are forks.
The `kristofmuys/OpenClaw_md` repo is his personal workspace config (this repo).

### 2. README.md: Missing Upstream Attribution

The "Related repos" section links only to Kris's forks. It should also reference
the upstream repos so the origin is clear.

---

## Placeholders That Still Need Real Values

| File | Field | Current Value | Needed |
|------|-------|---------------|--------|
| `USER.md` | Work email | `kris@example.com` | Real work/primary email |
| `TOOLS.md` | Telegram Group ID | `*(set after Telegram group is created)*` | Real group ID |
| `TOOLS.md` | Topic: Updates | `*(set after topic creation)*` | Real thread ID |
| `TOOLS.md` | Topic: Cron Updates | `*(set after topic creation)*` | Real thread ID |
| `TOOLS.md` | Topic: Knowledge Base | `*(set after topic creation)*` | Real thread ID |
| `TOOLS.md` | Topic: Self-Improvement | `*(set after topic creation)*` | Real thread ID |
| `TOOLS.md` | Topic: Dev | `*(set after topic creation)*` | Real thread ID |
| `MEMORY.md` | Personal email | `*(add when known)*` | Real personal email (optional) |

---

## Telegram Topics: Expand from 5 to 11

`TOOLS.md` has 5 topics. Prompt 11 (Messaging Setup) defines 11 topics that map
to the full feature set across all 26 build prompts.

**Current TOOLS.md (5 topics):**
Updates, Cron Updates, Knowledge Base, Self-Improvement, Dev

**Prompt 11 full set (11 topics):**
Daily Brief, Personal CRM, Email, Knowledge Base, Meta-Analysis,
Video Ideas, Earnings, Cron Updates, Financials, Health, Self-Improvement

The topic table in `TOOLS.md` should be expanded to match the features being built.

---

## Model Version

All workspace files reference `claude-sonnet-4-5`. The correct Anthropic API model ID
format uses dashes. If updating to Claude Sonnet 4.6, the API model ID would be
`claude-sonnet-4-6`.

**Files to update if model version changes:**
- `AGENTS.md` (Model Strategy section)
- `TOOLS.md` (Model Configuration section)
- `SUBAGENT-POLICY.md` (model references)
- `README.md` (Primary model line)
- `docs/WORKSPACE-FILES.md` (Prompting Best Practices header)

---

## BOOTSTRAP.md

Should be deleted after the first session completes (per its own instructions).

---

## Proposed Changes

### `MEMORY.md` (correction required)
Remove the false claim that Kris maintains/created OpenClaw. Replace with accurate
description: Kris runs OpenClaw (created by Matt Berman / mberman84) and maintains
his personal workspace config (`kristofmuys/OpenClaw_md`).

### `README.md` (correction required)
Add upstream repo references in the Related repos section:
- `mberman84/openclaw` - Original OpenClaw platform (upstream)
- `mberman84/awesome-openclaw-skills` - Original community skills (upstream)
- `mberman84/awesome-openclaw-usecases` - Original community use cases (upstream)

### `USER.md`
Replace `kris@example.com` with real work email.

### `TOOLS.md`
- Add Telegram Group ID
- Expand topic table from 5 to 11 topics
- Add all topic thread IDs
- Update model version if changing

### `AGENTS.md`, `SUBAGENT-POLICY.md`, `docs/WORKSPACE-FILES.md`
Update model version references if changing.

### `BOOTSTRAP.md`
Delete if first session is complete.

---

## What Does NOT Need to Change

- `SOUL.md`: Complete and well-written
- `HEARTBEAT.md`: Correct and concise
- `IDENTITY.md`: Clawd identity is set
- `SUBAGENT-POLICY.md`: Policy is correct (model name update only if version changes)
- `docs/WORKSPACE-FILES.md`: Content is correct (minor model name update if version changes)
- All 26 `prompts/*.md` files: Build prompts, not config. Correct as-is.
