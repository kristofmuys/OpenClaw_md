# TOOLS.md - Local Notes

Environment-specific values only (IDs, paths, and where secrets live).
Skills define how tools work. This file is for lookup values only.

## Secrets and config
- Canonical .env: ~/.openclaw/.env
- Platform config: ~/.openclaw/openclaw.json
- Workspace: ~/.openclaw/workspace

## Attribution
- When leaving permanent text (comments, messages, notes, code comments),
  prefix with "🦞 Clawd:" unless asked to ghostwrite.

## Primary Messaging Platform (Telegram)
- Group ID: *(set after Telegram group is created)*

| Topic | Thread ID | Behavior |
|-------|-----------|----------|
| Daily Brief | *(set after topic creation)* | cron-owned; respond to follow-ups only |
| Personal CRM | *(set after topic creation)* | contact queries and follow-up nudges |
| Email | *(set after topic creation)* | email queries and draft proposals |
| Knowledge Base | *(set after topic creation)* | KB ingestion and query notifications |
| Meta-Analysis | *(set after topic creation)* | business advisory council digests |
| Video Ideas | *(set after topic creation)* | video pitch discussion and feedback |
| Earnings | *(set after topic creation)* | financial tracking and earnings reports |
| Cron Updates | *(set after topic creation)* | cron-owned; failures only, success is silent |
| Financials | *(set after topic creation)* | financial data; never share outside DM or this topic |
| Health | *(set after topic creation)* | food logging and health tracking |
| Self-Improvement | *(set after topic creation)* | agent self-improvement and security alerts |

## Paths
- Logs: ~/.openclaw/workspace/data/logs/ (unified: all.jsonl)
- SQLite mirror: ~/.openclaw/workspace/data/logs.db
- Skills: ~/.openclaw/workspace/skills/
- Memory: ~/.openclaw/workspace/memory/

## API tokens
Stored in ~/.openclaw/.env. See .env.example for the canonical list.

## Voice Memos
- **Inbound:** User can send voice memos. The gateway auto-transcribes
  them to text.
- **Outbound:** Use the tts tool to reply as a voice note.
- **Rule:** Only reply with voice when explicitly asked. Default to text.

## Model Configuration
- Primary model: anthropic/claude-sonnet-4-6 (Anthropic Sonnet 4.6)
- Subagent model: anthropic/claude-sonnet-4-6 (Anthropic Sonnet 4.6)
- Fallback model: anthropic/claude-sonnet-4-6 (Anthropic)
- Gateway port: 18789
- Gateway mode: local (loopback only)

## Development Tools
- Node version: 22+
- Package manager: pnpm (preferred) or npm
- OpenClaw CLI: openclaw (global install via npm)
- Git: standard git CLI

## Content preferences
- Prefer concise, direct responses
- Code blocks for all code, commands, and file paths
- No markdown headers in conversational replies
- Inline code for short snippets, code blocks for multi-line
