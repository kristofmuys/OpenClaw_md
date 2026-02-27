# TOOLS.md - Local Notes

Environment-specific values only (IDs, paths, and where secrets live).
Skills define how tools work.

## Secrets and config
- Canonical .env: ~/.openclaw/.env
- Compatibility symlinks: ~/workspace/.env, ~/workspace/crm/.env
- Platform config: ~/.openclaw/openclaw.json

## Attribution
- When leaving permanent text (comments, messages, notes), prefix with
  "🦞 OpenClaw:" unless asked to ghostwrite

## Primary Messaging Platform (Telegram)
- Group ID: <your-telegram-group-id>

| Topic | Thread ID |
|-------|-----------|
| AI Updates | <id> |
| Cron Updates | <id> |
| Knowledge Base | <id> |
| Financials | <id> |
| Personal CRM | <id> |
| Self-Improvement | <id> |
| Health | <id> |

## Topic behavior (quick)
- Cron Updates: cron-owned; respond to follow-ups only
- Personal CRM: CRM queries and follow-ups
- Self-Improvement: failures only
- Financials: owner only; never share outside DM

## Secondary Platform (Slack)

| Channel | ID |
|---------|----|
| general | <channel-id> |
| ai-updates | <channel-id> |

## Project Management (Asana)
- Workspace: <workspace-name> (<workspace-id>)

| Project | ID |
|---------|-----|
| Main Project | <project-id> |
| Video Pipeline | <project-id> |

## Paths
- Email CLI: /usr/local/bin/gog (or your email tool path)
- Agent CLI: ~/.local/bin/agent (or your coding agent path)
- Logs: ~/workspace/data/logs/ (unified: all.jsonl),
  SQLite mirror: ~/workspace/data/logs.db

## API tokens
Stored in ~/.openclaw/.env. See .env.example for the canonical list.

## Voice Memos
- **Inbound:** User can send voice memos. The gateway auto-transcribes
  them to text.
- **Outbound:** Use the tts tool to reply as a voice note.
- **Rule:** Only reply with voice when explicitly asked. Default to text.

## Content preferences
- Prefer concise, direct responses
- Code blocks for all code and commands
- No markdown headers in conversational replies

## Dual prompt stack
- Default: root .md files (claude-sonnet-4-5)
- Fallback: codex-prompts/ (claude-haiku-4-5, loaded when active)
- Switching is configured in your agent framework's config and requires
  a gateway restart

## Model Configuration
- Primary model: claude-sonnet-4-5 (Anthropic)
- Subagent model: claude-sonnet-4-5 (Anthropic)
- Fallback model: claude-haiku-4-5 (Anthropic)
- Gateway port: 18789
