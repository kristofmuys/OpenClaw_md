# OpenClaw Setup Plan

## Status: Awaiting User Input

This document captures the full analysis of the current repo state, all identified issues,
and the questions that must be answered before changes can be made correctly.

---

## What OpenClaw Is

OpenClaw is a personal AI assistant platform that:
- Runs a local gateway process that connects to messaging platforms (Telegram, Slack)
- Loads workspace `.md` files as the agent's system prompt on every session
- Supports skills (modular capabilities), cron jobs, subagents, and memory files
- Uses Claude (Anthropic) as the primary LLM via OAuth or API key
- Is configured via `~/.openclaw/openclaw.json` and `~/.openclaw/.env`

The workspace files in this repo ARE the agent's "brain" - they define identity,
rules, tools, and memory. Getting them right is the entire point.

---

## Current Repo Structure

```
Root workspace files (loaded every session):
  AGENTS.md         - Rules of engagement
  SOUL.md           - Personality
  IDENTITY.md       - Name (Clawd), emoji (lobster)
  USER.md           - About the user
  TOOLS.md          - Environment config (IDs, paths)
  HEARTBEAT.md      - Hourly health check checklist
  MEMORY.md         - Synthesized preferences (private chats only)
  BOOTSTRAP.md      - First-run ritual (delete after use)
  SUBAGENT-POLICY.md - When to spawn subagents

Reference/docs:
  docs/WORKSPACE-FILES.md  - Guide to file loading rules
  prompts/01-26.md         - 26 build prompts for implementing features
```

---

## Issues Found: Placeholders Still Needing Real Values

### CRITICAL - Must be resolved before onboarding

| File | Line | Current Value | Issue |
|------|------|---------------|-------|
| `USER.md` | 12 | `kris@example.com` | Placeholder email - needs real work email |
| `MEMORY.md` | 6 | `*(add when known)*` | Personal email placeholder |
| `TOOLS.md` | 16 | `*(set after Telegram group is created)*` | Telegram Group ID |
| `TOOLS.md` | 20-24 | `*(set after topic creation)*` x5 | All 5 topic thread IDs |
| `README.md` | 35,55-57 | `kristofmuys` | Wrong GitHub username throughout |
| `MEMORY.md` | 42-45 | `kristofmuys/openclaw` etc. | Wrong GitHub username for repos |

### IMPORTANT - Incorrect assumptions by previous agents

| File | Issue | Notes |
|------|-------|-------|
| `USER.md` | Says Kris "maintains the OpenClaw project" | Template assumption - may not be accurate |
| `USER.md` | Says "Developer and OpenClaw contributor" | May not be accurate |
| `TOOLS.md` | Only 5 Telegram topics listed | Prompt 11 suggests 11 topics - inconsistent |
| `IDENTITY.md` | Avatar `*(none yet)*` | Minor - can stay as placeholder |
| All files | Model `claude-sonnet-4-5` | Need to confirm correct model version |

### MINOR - Style/consistency issues

| File | Issue |
|------|-------|
| `docs/WORKSPACE-FILES.md` | Section header says "Claude Sonnet 4.5" - should match chosen model |
| `TOOLS.md` | Gateway port 18789 - is this the correct default? |

---

## Issues Found: Incorrect Agent Assumptions

### 1. GitHub Username (CRITICAL)
The gists are from `mberman84`. The entire repo uses `kristofmuys` as the GitHub
username. This appears to be because the agents copied from a template that used
`kristofmuys` (who appears to be a different OpenClaw user) without updating it.

**Files affected:** `README.md` (lines 35, 55-57), `MEMORY.md` (lines 42-45)

### 2. Telegram Topics Mismatch
`TOOLS.md` lists 5 topics: Updates, Cron Updates, Knowledge Base, Self-Improvement, Dev.
`prompts/11-messaging-setup.md` lists 11 topics: Daily Brief, Personal CRM, Email,
Knowledge Base, Meta-Analysis, Video Ideas, Earnings, Cron Updates, Financials, Health,
Self-Improvement.

The agents picked 5 topics without consulting the user. The correct set depends on
which features the user actually wants to implement.

### 3. Model Version Confusion
The user mentioned agents confused Sonnet 4.5 and 4.6. The current files all use
`claude-sonnet-4-5`. The correct Anthropic API model IDs are:
- `claude-sonnet-4-5` = Claude Sonnet 4.5 (released ~2025)
- `claude-sonnet-4-6` would be 4.6 if it exists

The model running this planning session is `anthropic/claude-sonnet-4.6` (note the
dot notation used by the platform vs. the dash notation used in API calls).

### 4. USER.md Context
The template says Kris "maintains the OpenClaw project and related repositories."
This was copied from a template for the OpenClaw creator. If the user is Matt Berman
(mberman84), this is accurate. If not, it needs to be corrected.

---

## Questions That Must Be Answered

These are listed in priority order. The first 4 are blocking - nothing can be
correctly configured without them.

### Q1: GitHub Username
**Current:** `kristofmuys` everywhere
**Question:** Is your GitHub username `mberman84`?
**Impact:** README.md, MEMORY.md repo references

### Q2: Are you Matt Berman / the OpenClaw creator?
**Question:** The gists are from `mberman84`. Are you Matt Berman, the creator of
OpenClaw? This affects how USER.md describes your relationship to the project.
**Impact:** USER.md context section

### Q3: Work Email
**Current:** `kris@example.com`
**Question:** What is your actual work/primary email address?
**Impact:** USER.md

### Q4: Model Version
**Current:** `claude-sonnet-4-5` everywhere
**Question:** Which Claude model do you want as primary? Options:
- `claude-sonnet-4-5` (Sonnet 4.5 - the current stable)
- `claude-opus-4-5` (Opus 4.5 - more capable, more expensive)
- Other?
**Impact:** AGENTS.md, TOOLS.md, SUBAGENT-POLICY.md, README.md, docs/WORKSPACE-FILES.md

### Q5: Telegram Group Setup
**Current:** All IDs are placeholders
**Question:** Has your Telegram group been created? If yes, provide:
- Group ID (negative number like `-1001234567890`)
- Thread IDs for each topic you want
**Impact:** TOOLS.md

### Q6: Telegram Topics
**Current:** TOOLS.md has 5 topics; Prompt 11 suggests 11
**Question:** Which topics do you want? Suggested full set based on your prompts:
- Daily Brief
- Personal CRM
- Email
- Knowledge Base
- Meta-Analysis (Business Advisory Council)
- Video Ideas
- Earnings
- Cron Updates
- Financials
- Health
- Self-Improvement
- Dev
**Impact:** TOOLS.md topic table

### Q7: Personal Email
**Current:** `*(add when known)*` in MEMORY.md
**Question:** Do you want to add your personal email now?
**Impact:** MEMORY.md (private chats only - safe to add)

### Q8: Meeting Recorder
**Question:** Do you use Fathom, Otter, Fireflies, or another meeting recorder?
**Impact:** prompts/02-meeting-intelligence.md

### Q9: Task Manager
**Question:** You have a dedicated Asana prompt (25). Is Asana your primary task
manager, or do you also use Linear/Todoist?
**Impact:** prompts/02, 07 references to task manager

---

## Proposed Changes (Once Questions Answered)

### README.md
- Replace `kristofmuys` with correct GitHub username
- Update repo links to point to actual forked repos
- Update model version reference

### USER.md
- Replace `kris@example.com` with real work email
- Update context section to accurately describe user's role
- Confirm timezone (US/Eastern is currently set - is this correct?)

### MEMORY.md
- Replace `kristofmuys/openclaw` etc. with correct repo references
- Add personal email if provided

### TOOLS.md
- Add Telegram Group ID when available
- Add all topic thread IDs when available
- Expand topic table to match the full set of topics from Prompt 11
- Confirm gateway port 18789

### AGENTS.md
- Update model version if different from `claude-sonnet-4-5`

### SUBAGENT-POLICY.md
- Update model version references if different

### docs/WORKSPACE-FILES.md
- Update "Claude Sonnet 4.5" header to match chosen model

---

## What Does NOT Need to Change

The following files appear correct and complete as-is:
- `SOUL.md` - personality content is well-written and complete
- `HEARTBEAT.md` - checklist is appropriate
- `BOOTSTRAP.md` - first-run ritual is correct
- `IDENTITY.md` - Clawd identity is set (avatar placeholder is fine)
- `SUBAGENT-POLICY.md` - policy is well-defined (just model name to update)
- All 26 `prompts/*.md` files - these are build prompts, not config files.
  They contain generic "your X" language intentionally. The specific ones
  (meeting recorder, task manager) can be updated once confirmed.
- `docs/WORKSPACE-FILES.md` - content is correct (minor model name update)

---

## OpenClaw Installation Notes

Based on the workspace files, the setup sequence is:
1. Install OpenClaw: `npm install -g openclaw`
2. Clone this repo to `~/.openclaw/workspace`
3. Configure `~/.openclaw/openclaw.json`
4. Set up `~/.openclaw/.env` with API tokens
5. Run `openclaw gateway start`
6. Pair Telegram: `openclaw pairing approve telegram <code>`
7. Create Telegram topics, update TOOLS.md with IDs
8. Run `openclaw onboard` (or let BOOTSTRAP.md guide first session)

The BOOTSTRAP.md file should be deleted after the first session completes.

---

## Next Steps

1. User answers the questions above
2. Make targeted edits to the files listed in "Proposed Changes"
3. Verify consistency across all files
4. Confirm repo is ready for `openclaw onboard`
