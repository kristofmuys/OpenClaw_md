# PRD.md - Product Requirements & Feature Inventory

> Everything built on top of the base OpenClaw platform. Canonical reference for what exists, where it lives, and how it works.
> Operational use cases and workflow playbooks live in `docs/USE-CASES-WORKFLOWS.md`.

---

## Table of Contents

1. [Architecture Overview](#architecture-overview)
2. [OpenClaw Platform Configuration](#openclaw-platform-configuration)
3. [Skills](#skills)
4. [Shared Modules](#shared-modules)
5. [Scripts & Automations](#scripts--automations)
6. [Cron Jobs](#cron-jobs)
7. [Memory System](#memory-system)
8. [Integrations](#integrations)
9. [Databases](#databases)
10. [Environment Variables](#environment-variables)
11. [Configuration Files](#configuration-files)

---

## Architecture Overview

The workspace is a monorepo-style project layered on top of OpenClaw. The base platform provides the agent framework, gateway, and skill system. Everything below is custom.

```
workspace/
├── data/                 # Workspace databases (cron-log, interactions)
├── docs/                 # Setup guides and documentation
├── memory/               # Daily notes, state files, reference data
├── reference/            # Static reference data
├── scripts/              # Shell automation scripts
├── shared/               # Shared Node.js utility modules
├── skills/               # OpenClaw skills
├── state/                # Mutable runtime state files
├── tests/                # Test suite
├── tools/                # Standalone utility scripts and databases
├── .learnings/           # Self-improvement corrections and learnings
└── [Root .md files]      # Core config (AGENTS, TOOLS, MEMORY, SOUL, etc.)
```

**Key patterns:**
- SQLite for all persistent local data (WAL mode, foreign keys)
- Vector embeddings for semantic search
- Telegram as the primary notification and interaction channel
- All cron jobs logged to a central database with Telegram notifications
- Shared modules (`shared/`) for common functionality across tools and skills

---

## OpenClaw Platform Configuration

**Config location:** `~/.openclaw/`
**Version:** Latest stable

### Gateway

- **Port:** 18789
- **Mode:** Local (loopback only, not exposed to network)
- **Auth:** Token-based
- **Logs:** `~/.openclaw/logs/gateway.log` and `gateway.err.log`
- **Launchd/systemd:** RunAtLoad + KeepAlive (auto-restart)

### Model Providers

| Provider | Models | Context |
|----------|--------|---------|
| Anthropic | claude-sonnet-4-5 (primary), claude-haiku-4-5 | 200K |

**Model fallback chain:**
- Main: claude-sonnet-4-5 → claude-haiku-4-5
- Subagents: claude-sonnet-4-5 → claude-haiku-4-5

### Agent Settings

- Primary model: `anthropic/claude-sonnet-4-5`
- Max concurrent agents: 4
- Max concurrent subagents: 8
- Subagent primary model: claude-sonnet-4-5
- Context pruning: cache-ttl mode, 1h TTL
- Heartbeat interval: 1 hour
- Memory backend: `builtin`

### Plugins

| Plugin | Status | Purpose |
|--------|--------|---------|
| `telegram` | Enabled | Telegram channel integration |
| `slack` | Enabled | Slack channel integration (socket mode) |
| `memory-core` | Enabled | Core memory backend |

### Channels

- **Telegram:** DM policy "pairing", group allowlist, partial stream mode
- **Slack:** Socket mode, allowlist policy, history limit 50

---

## Skills

Skills are installed via the `clawdhub` CLI and stored in `~/workspace/skills/`.

### Installed Skills

| Skill | Purpose |
|-------|---------|
| `knowledge-base` | RAG knowledge base with semantic search |
| `crm-query` | Personal CRM natural language interface |
| `humanizer` | Strip AI writing patterns from text |
| `web-search` | Web search via Brave Search API |
| `browser-control` | Browser automation for web scraping |

---

## Shared Modules

| Module | Purpose |
|--------|---------|
| `shared/llm-router.js` | Unified LLM routing layer |
| `shared/interaction-store.js` | SQLite call logger |
| `shared/anthropic-agent-sdk.js` | Anthropic SDK wrapper with OAuth |
| `shared/model-utils.js` | Model name utilities and aliases |
| `shared/notification-redaction.js` | PII redaction for outbound messages |
| `shared/event-log.js` | Structured event logging |

---

## Scripts & Automations

| Script | Purpose |
|--------|---------|
| `scripts/auto-git-sync.sh` | Hourly git auto-sync |
| `scripts/backup-databases.sh` | Hourly encrypted database backup |
| `scripts/restore-databases.sh` | Database restore from backup |
| `scripts/disk-space-check.sh` | Weekly disk space monitoring |
| `scripts/rotate-logs.sh` | Daily log rotation |
| `scripts/system-health-check.sh` | System health check |

---

## Cron Jobs

### Daily Jobs

| Job | Schedule | Purpose |
|-----|----------|---------|
| Morning Briefing | 7am UTC | Daily briefing with calendar and tasks |
| Git Backup | Every hour | Auto-commit workspace changes |
| Database Backup | Every hour | Encrypted backup to cloud storage |
| System Health Check | Every hour | Gateway and service health |

### Weekly Jobs

| Job | Schedule | Purpose |
|-----|----------|---------|
| Weekly Disk Space Check | Sunday 2am UTC | Check disk space, alert if below 20GB |
| Security Review | Saturday 3:30am UTC | Automated security audit |

---

## Memory System

**Location:** `memory/`

### Structure

| Path | Purpose |
|------|---------|
| `memory/YYYY-MM-DD.md` | Daily notes - raw capture of conversations, events, tasks. Written first, always. |
| `MEMORY.md` (root) | Synthesized wisdom - distilled patterns, preferences, lessons. Only loaded in direct chats. |
| `memory/heartbeat-state.json` | Heartbeat check timestamps |

### How It Works

- **Write first:** Daily notes (`YYYY-MM-DD.md`) capture everything in the moment
- **Synthesize weekly:** Cron job distills daily notes into `MEMORY.md`
- **Heartbeat tracking:** Checks stored in `heartbeat-state.json` with timestamps for each check type

---

## Integrations

### Telegram

- **Group ID:** `<your-telegram-group-id>`
- **Primary interface** for notifications, approvals, and cron updates

| Topic | ID | Purpose |
|-------|-----|---------|
| AI Updates | <id> | AI-related updates and news |
| Cron Updates | <id> | Automated cron job notifications |
| Knowledge Base | <id> | KB ingestion and querying |
| Financials | <id> | Financial data (confidential) |
| Personal CRM | <id> | Contact management |
| Self-Improvement | <id> | Agent self-improvement |
| Health | <id> | Health tracking |

### Slack

| Channel | ID | Purpose |
|---------|-----|---------|
| general | <channel-id> | General communication |
| ai-updates | <channel-id> | AI trend tracking |

**Auth:** Bot token + user token
**Attribution:** Bot messages no prefix; user token messages prefix with `🦞 OpenClaw:`

### Google Workspace (via `gog` CLI)

- **CLI Location:** `/usr/local/bin/gog`
- **Services:** Gmail, Calendar, Drive, Docs, Sheets
- **Auth:** OAuth tokens in `~/Library/Application Support/gogcli/`

---

## Databases

All databases are SQLite with WAL mode enabled.

| Database | Location | Purpose |
|----------|----------|---------|
| Cron Log | `~/workspace/data/cron-log.db` | Cron job run history |
| Interactions | `~/workspace/data/interactions.db` | All API calls and LLM interactions |
| Structured Logs | `~/workspace/data/logs.db` | Query-friendly mirror of structured logs |
| Knowledge Base | `skills/knowledge-base/data/knowledge.db` | RAG content with embeddings |

**Backup:** Hourly via `backup-databases.sh`, keeps last 7 backups.

---

## Environment Variables

### Canonical `.env` (`~/.openclaw/.env`)

| Variable | Purpose |
|----------|---------|
| `ANTHROPIC_API_KEY` | Anthropic API key (or use OAuth) |
| `CLAUDE_CODE_OAUTH_TOKEN` | Anthropic OAuth token (preferred) |
| `BRAVE_API_KEY` | Brave Search API key |
| `SLACK_APP_TOKEN` | Slack app-level token |
| `SLACK_BOT_TOKEN` | Slack bot token |
| `SLACK_USER_TOKEN` | Slack user token |
| `OPENCLAW_GATEWAY_TOKEN` | Gateway auth token |
| `TELEGRAM_BOT_TOKEN` | Telegram bot token |

---

## Configuration Files

Root-level `.md` files that define workspace behavior:

| File | Purpose |
|------|---------|
| `AGENTS.md` | Rules of engagement - safety, security, task execution, model strategy |
| `SOUL.md` | Personality - direct communication, real opinions, brevity mandatory |
| `IDENTITY.md` | Identity - name: OpenClaw Assistant, creature: AI with lobster energy, emoji: 🦞 |
| `USER.md` | User info - timezone, email accounts |
| `TOOLS.md` | Environment config - channel IDs, API token locations, tool paths |
| `MEMORY.md` | Synthesized preferences - user preferences, workflow patterns, operational lessons |
| `HEARTBEAT.md` | Periodic checklist - security audit, gateway check, error log scan |
| `SUBAGENT-POLICY.md` | Subagent policy - when to use, failure handling |
| `PRD.md` | This file - full feature inventory |

---

*Last updated: 2026-02-27 (Initial OpenClaw installation)*
