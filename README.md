# OpenClaw_md

Personal OpenClaw workspace files for Kris's AI assistant setup.

## What's in here

These are the workspace files that OpenClaw loads as the agent's system prompt.
They define how the agent behaves, who it is, and what it knows about the environment.

### Root workspace files (loaded every session)

| File | Purpose |
|------|---------|
| `AGENTS.md` | Rules of engagement: security, data handling, communication style, task execution |
| `SOUL.md` | Personality and communication style |
| `IDENTITY.md` | Agent name (Clawd), emoji (🦞), character notes |
| `USER.md` | About Kris: timezone, email accounts, context |
| `TOOLS.md` | Local environment: channel IDs, paths, model config |
| `HEARTBEAT.md` | Periodic health check checklist |
| `SUBAGENT-POLICY.md` | When to spawn subagents vs. handle directly |
| `MEMORY.md` | Synthesized preferences (loaded in private chats only) |
| `BOOTSTRAP.md` | First-run ritual (delete after completion) |

### Reference files

| File | Purpose |
|------|---------|
| `docs/WORKSPACE-FILES.md` | Guide to workspace file organization and loading rules |
| `prompts/` | 26 build prompts for implementing OpenClaw features |

## Setup

1. Clone this repo into your OpenClaw workspace:
   ```bash
   git clone https://github.com/kristofmuys/OpenClaw_md.git ~/.openclaw/workspace
   ```

2. Or configure OpenClaw to use this directory:
   ```json
   { "agent": { "workspace": "/path/to/OpenClaw_md" } }
   ```

3. Update `TOOLS.md` with your actual Telegram group ID and topic IDs.

4. Update `USER.md` with your actual email and timezone.

5. Run `openclaw onboard` if you haven't already.

## Model

Primary model: `claude-sonnet-4-5` (Anthropic)

## Related repos

OpenClaw was created by Matt Berman (mberman84). These are Kris's forks:

- [kristofmuys/openclaw](https://github.com/kristofmuys/openclaw) - The OpenClaw platform (fork)
- [kristofmuys/awesome-openclaw-skills](https://github.com/kristofmuys/awesome-openclaw-skills) - Community skills (fork)
- [kristofmuys/awesome-openclaw-usecases](https://github.com/kristofmuys/awesome-openclaw-usecases) - Community use cases (fork)

Upstream (original):

- [mberman84/openclaw](https://github.com/mberman84/openclaw) - Original OpenClaw platform
- [mberman84/awesome-openclaw-skills](https://github.com/mberman84/awesome-openclaw-skills) - Original community skills
- [mberman84/awesome-openclaw-usecases](https://github.com/mberman84/awesome-openclaw-usecases) - Original community use cases
