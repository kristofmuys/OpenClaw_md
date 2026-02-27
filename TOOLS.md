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

| Topic | Thread ID |
|-------|-----------|
| Updates | *(set after topic creation)* |
| Cron Updates | *(set after topic creation)* |
| Knowledge Base | *(set after topic creation)* |
| Self-Improvement | *(set after topic creation)* |
| Dev | *(set after topic creation)* |

## Topic behavior (quick)
- Cron Updates: cron-owned; respond to follow-ups only
- Self-Improvement: failures and security alerts only
- Dev: code discussions, debugging, project updates
- Updates: general status updates and announcements

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
- Primary model: claude-sonnet-4-5 (Anthropic)
- Subagent model: claude-sonnet-4-5 (Anthropic)
- Fallback model: claude-haiku-4-5 (Anthropic)
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
