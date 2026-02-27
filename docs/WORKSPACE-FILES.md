# Workspace File Guide

Core workspace `.md` files are injected into the LLM system prompt on most requests, with some files loaded conditionally by context. Size still directly impacts token cost, so keep files focused and avoid duplication across files.

## PRD vs workflows vs workspace file guide

These three docs answer different questions:

| File | Primary question it answers | What belongs here | What should not go here |
|------|-----------------------------|-------------------|-------------------------|
| `PRD.md` | What exists in the workspace, and where is it implemented? | Technical inventory, architecture map, component/module lists, scripts, databases, config surfaces, integration inventory | Step-by-step operational playbooks and long narrative workflow descriptions |
| `docs/USE-CASES-WORKFLOWS.md` | How is the system used in practice? | Major use cases, trigger -> flow -> output behavior, custom workflow patterns, failure handling expectations | Deep implementation detail that duplicates PRD component tables |
| `docs/WORKSPACE-FILES.md` | How should docs be organized and loaded into prompts? | File-loading behavior, scope boundaries between root docs, source-of-truth map, anti-duplication guidance | Product inventory details and workflow internals |

Quick rule:
- If you are listing systems and files, update `PRD.md`.
- If you are describing behavior and handoffs, update `docs/USE-CASES-WORKFLOWS.md`.
- If you are changing documentation ownership rules, update `docs/WORKSPACE-FILES.md`.

## Where these files should live

- Keep `PRD.md` in the repo root. It is a canonical top-level reference and is already used by existing pointers and routines.
- Keep `docs/USE-CASES-WORKFLOWS.md` in `docs/` because it is detailed operational documentation that is read on demand.
- Keep `docs/WORKSPACE-FILES.md` in `docs/` because it is documentation-governance guidance, not a runtime prompt file.

## Files Loaded Every Request

These are assembled into the system prompt by OpenClaw on every turn. Truncated at ~20,000 chars total.

| File | Purpose | Scope | Guidelines |
|------|---------|-------|------------|
| **AGENTS.md** | Workspace rules of engagement | Task execution, safety, message patterns, group chat behavior, subagent policy | Operational rules only. Don't duplicate content from TOOLS.md, SOUL.md, or HEARTBEAT.md - reference them instead. |
| **SOUL.md** | Personality and identity philosophy | Core truths, boundaries, vibe, continuity | Keep philosophical and concise. This is *who* the agent is, not *what* it does. Don't put operational rules here. |
| **IDENTITY.md** | Agent identity metadata | Name, creature type, vibe, emoji, avatar | 5-10 lines max. Just the facts. |
| **USER.md** | Information about the human | Name, timezone, email accounts, preferences | Personal info only. Don't put workflow rules here. |
| **TOOLS.md** | Local setup notes | Environment-specific config: channel IDs, API tokens, project IDs, device names, tool locations | **NOT for tool documentation.** Skills have their own `SKILL.md`. Agents can run `--help`. Only put setup-specific values here (IDs, paths, credentials, topic behavior guides). |
| **HEARTBEAT.md** | Heartbeat checklist | What to check during periodic heartbeat polls | Keep tiny - this runs every hour. Short checklist only, no essays. |

## Files Loaded Conditionally

| File | Purpose | When Loaded |
|------|---------|-------------|
| **MEMORY.md** | Curated long-term memory | Main session only (direct chats). Loaded only in direct contexts - excluded from group/shared contexts because it contains personal info. |
| **SUBAGENT-POLICY.md** | Subagent spawning rules | Referenced by AGENTS.md. Loaded when subagent decisions are needed. |
| **RESTORE.md** | Instance recreation instructions | Only when setting up a new machine. Not loaded in normal operation. |

## Files NOT Loaded into Prompts

| File | Purpose |
|------|---------|
| `memory/YYYY-MM-DD.md` | Daily notes - raw logs of what happened each day. Read on demand. |
| `memory/heartbeat-state.json` | Heartbeat check timestamps. Read/written during heartbeats. |
| `skills/*/SKILL.md` | Skill documentation - loaded on demand when the skill is invoked. |
| `reference/*.md` | Reference data. Read on demand. |
| `.learnings/LEARNINGS.md` | Captured corrections and insights. Read on demand. |
| `PRD.md` | Product requirements and full feature inventory. Too large for injection - read on demand. |
| `docs/USE-CASES-WORKFLOWS.md` | Operational guide for major use cases, custom behavior, and workflow playbooks. Read on demand. |
| `docs/*.md` | Documentation (this file, setup guides, etc.). Not injected into prompts. |
| `tests/*.md` | Test documentation. Not injected into prompts. |

## Key Rules

1. **No duplication across files.** If a rule exists in AGENTS.md, reference the source file in MEMORY.md or TOOLS.md instead of repeating it.
2. **TOOLS.md is for local notes, not documentation.** It answers "what are my channel IDs?" not "how does the skill work?"
3. **MEMORY.md is for learned patterns, not restated rules.** It answers "what has the user told me they prefer?" not "what does AGENTS.md say?"
4. **Keep files small.** Every line costs tokens on every request (except conditionally-loaded files). Ask: "Does the agent need this on *every* turn, or only sometimes?"
5. **Skills are self-documenting.** Each skill has a `SKILL.md` loaded on demand - TOOLS.md focuses on environment-specific setup instead.

## Prompting Best Practices (Claude Sonnet 4.5)

Key points for quick reference:

- Use natural language, not ALL-CAPS urgency markers - Claude overtriggers on aggressive emphasis
- Tell it what to do, not what not to do - positive framing is more effective
- Explain *why*, not just *what* - the model generalizes from explanations
- Match prompt style to desired output - heavy markdown in prompts encourages heavy markdown in responses

## Source of Truth

| Topic | Canonical File |
|-------|---------------|
| Subagent timing threshold | `SUBAGENT-POLICY.md` |
| Message consolidation pattern | `AGENTS.md` |
| Model tiers / selection | `AGENTS.md` (brief) |
| Attribution rules | `TOOLS.md` (`## Attribution`) |
| Telegram topic behavior | `TOOLS.md` (Topic Behavior Guide) |
| Heartbeat checklist | `HEARTBEAT.md` |
| Personality / communication style | `SOUL.md` |
| Agent identity | `IDENTITY.md` |
| User info / timezone | `USER.md` |
| Learned preferences | `MEMORY.md` |
| Major use cases / workflows | `docs/USE-CASES-WORKFLOWS.md` |
