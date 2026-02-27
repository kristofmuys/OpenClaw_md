# Workspace File Guide

Core workspace `.md` files are injected into the LLM system prompt on most requests,
with some files loaded conditionally by context. Size directly impacts token cost,
so keep files focused and avoid duplication across files.

## File Loading Behavior

### Files Loaded Every Request

These are assembled into the system prompt by OpenClaw on every turn.
Truncated at ~20,000 chars total.

| File | Purpose | Scope | Guidelines |
|------|---------|-------|------------|
| **AGENTS.md** | Workspace rules of engagement | Task execution, safety, message patterns, group chat behavior, subagent policy | Operational rules only. Don't duplicate content from TOOLS.md, SOUL.md, or HEARTBEAT.md. |
| **SOUL.md** | Personality and identity philosophy | Core truths, boundaries, vibe, continuity | Keep philosophical and concise. This is *who* the agent is, not *what* it does. No operational rules here. |
| **IDENTITY.md** | Agent identity metadata | Name, creature type, vibe, emoji, avatar | 5-10 lines max. Just the facts. |
| **USER.md** | Information about Kris | Name, timezone, email accounts, preferences | Personal info only. No workflow rules here. |
| **TOOLS.md** | Local setup notes | Environment-specific config: channel IDs, API tokens, project IDs, tool locations | NOT for tool documentation. Only put setup-specific values here (IDs, paths, credentials). |
| **HEARTBEAT.md** | Heartbeat checklist | What to check during periodic heartbeat polls | Keep tiny. Short checklist only, no essays. |

### Files Loaded Conditionally

| File | Purpose | When Loaded |
|------|---------|-------------|
| **MEMORY.md** | Curated long-term memory | Direct chats with Kris only. Excluded from group/shared contexts because it contains personal info. |
| **SUBAGENT-POLICY.md** | Subagent spawning rules | Referenced by AGENTS.md. Loaded when subagent decisions are needed. |
| **BOOTSTRAP.md** | First-run ritual | Only on first session of a new workspace. Delete after completion. |

### Files NOT Loaded into Prompts

| File | Purpose |
|------|---------|
| `memory/YYYY-MM-DD.md` | Daily notes - raw logs of what happened each day. Read on demand. |
| `memory/heartbeat-state.json` | Heartbeat check timestamps. Read/written during heartbeats. |
| `skills/*/SKILL.md` | Skill documentation - loaded on demand when the skill is invoked. |
| `reference/*.md` | Reference data. Read on demand. |
| `.learnings/LEARNINGS.md` | Captured corrections and insights. Read on demand. |
| `docs/*.md` | Documentation (this file, setup guides, etc.). Not injected into prompts. |
| `prompts/*.md` | Build prompts for implementing features. Not injected into prompts. |

## Key Rules

1. **No duplication across files.** If a rule exists in AGENTS.md, reference the source file
   in MEMORY.md or TOOLS.md instead of repeating it.
2. **TOOLS.md is for local notes, not documentation.** It answers "what are my channel IDs?"
   not "how does the skill work?"
3. **MEMORY.md is for learned patterns, not restated rules.** It answers "what has Kris told
   me he prefers?" not "what does AGENTS.md say?"
4. **Keep files small.** Every line costs tokens on every request (except conditionally-loaded
   files). Ask: "Does the agent need this on *every* turn, or only sometimes?"
5. **Skills are self-documenting.** Each skill has a `SKILL.md` loaded on demand.
   TOOLS.md focuses on environment-specific setup instead.

## Prompting Best Practices (Claude Sonnet 4.5)

Key points for quick reference:

- Use natural language, not ALL-CAPS urgency markers. Claude overtriggers on aggressive emphasis.
- Tell it what to do, not what not to do. Positive framing is more effective.
- Explain *why*, not just *what*. The model generalizes from explanations.
- Match prompt style to desired output. Heavy markdown in prompts encourages heavy markdown in responses.
- Avoid em dashes in prompts. They're a recognized AI writing tell.

## Source of Truth

| Topic | Canonical File |
|-------|---------------|
| Subagent timing threshold | `SUBAGENT-POLICY.md` |
| Message consolidation pattern | `AGENTS.md` |
| Model tiers / selection | `AGENTS.md` (brief) + `TOOLS.md` (model config) |
| Attribution rules | `TOOLS.md` (`## Attribution`) |
| Telegram topic behavior | `TOOLS.md` (Topic behavior section) |
| Heartbeat checklist | `HEARTBEAT.md` |
| Personality / communication style | `SOUL.md` |
| Agent identity | `IDENTITY.md` |
| User info / timezone | `USER.md` |
| Learned preferences | `MEMORY.md` |
