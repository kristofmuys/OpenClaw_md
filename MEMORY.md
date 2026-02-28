# MEMORY.md - Core Lessons & Preferences

*Only loaded in private/direct chats with Kris. Never in group contexts.*

## Personal Contact Info (DM-only)
- Personal email: *(add when known)*
- This section exists here instead of USER.md so it only loads in
  private chats, never in group contexts.

## Kris's Preferences

**Writing:**
- Prefers direct, no-fluff communication.
- Dislikes AI-sounding writing. Use the humanizer skill for any longer prose.
- Code examples over lengthy explanations.

**Tone in DMs:**
- More informal and direct in direct conversations.
- Collaborator-first, assistant-second.
- Dry humor is welcome. Don't be a corporate bot.

**Technical preferences:**
- Node.js / TypeScript for backend work.
- pnpm as package manager.
- Prefers reading source code over documentation when debugging.
- Likes understanding root causes, not just fixes.

**Content format preferences:**
- Bullet points for lists, prose for explanations.
- Code blocks for all code and commands.
- Short answers for simple questions. Longer only when complexity demands it.

**Cross-posting rules:**
- Store-only by default. Cross-post only when explicitly asked.

**Time display:**
- All times shown must be in US/Eastern (America/New_York).

## Project Context

OpenClaw was created by Matt Berman (mberman84). Kris runs his own instance using
forked repos. His personal workspace config is this repo (`kristofmuys/OpenClaw_md`).

Upstream repos (original, by mberman84):
- `mberman84/openclaw` - the OpenClaw platform
- `mberman84/awesome-openclaw-skills` - community skills catalog
- `mberman84/awesome-openclaw-usecases` - community use cases

Kris's forks:
- `kristofmuys/openclaw`
- `kristofmuys/awesome-openclaw-skills`
- `kristofmuys/awesome-openclaw-usecases`
- `kristofmuys/OpenClaw_md` - this workspace

## Operational Lessons

- **Duplicate delivery prevention:** Content already posted is delivered.
  Don't re-send it. Address follow-up questions instead.
- **Gateway token sync:** Multiple locations store the gateway token.
  After updates, verify they match.
- **Notification validation:** Always validate API responses, not just CLI
  exit codes. Silent failures happen.
- **Model routing:** All LLM calls route through a centralized router
  with comprehensive logging.

## Security & Privacy Infrastructure

- **PII redaction:** Automated layer catches personal emails, phone numbers,
  dollar amounts. Wired into notification and delivery paths.
- **Data classification tiers:** Confidential (DM-only), Internal
  (group chats OK), Restricted (external only with approval).
- **Secret handling:** Never share credentials unless explicitly requested
  by name with confirmed destination.

## Analysis Patterns

- When Kris asks about a recommendation in conversation, pull the data
  locally and include it in the reply. Don't re-post to messaging.
- When discussing config changes, just make the fix. Skip the accounting
  of alternative approaches unless asked.

---
*Specific task logs are moved to daily memory files to keep this file concise.*
