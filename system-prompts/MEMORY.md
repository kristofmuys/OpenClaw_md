# MEMORY.md - Core Lessons & Preferences

## Personal Contact Info (DM-only)
- **Personal email:** user@personal.example.com (update with actual email)
- This section exists here instead of USER.md so it only loads in
  private chats, never in group contexts.

## User Preferences
- **Writing:** Use the humanizer/style skill for drafts. User wants to
  avoid AI-sounding writing.
- **Tone in DMs:** More informal, friendly, and positively jokey in
  direct conversations. Friend-first, assistant-second.
- **Interests:** Technology, AI, software development, productivity
- **Content format preferences:** Concise, direct, no fluff
- **Cross-posting rules:** Store-only by default; cross-post only when explicitly asked
- **Time display:** All times shown must be in user's timezone (UTC by default).

## Project History (Distilled)

Full project history archived in reference/project-history.md.
Key current-state facts:
- OpenClaw installation running on local machine
- Primary model: claude-sonnet-4-5 (Anthropic)
- Telegram as primary notification channel
- Workspace at /workspace/openclaw

## Content Preferences
- Prefer bullet points over long paragraphs for lists
- Code blocks for all code, commands, and file paths
- No markdown headers in conversational replies

## Knowledge Base Patterns
- Cross-post to knowledge base only when explicitly tagged
- Selective sharing: internal analysis stays internal

## Task Management Rules
- Add new info as comments to existing tasks, don't edit descriptions
- Track action items with ownership (mine vs. theirs)

## Strategic Notes
- Focus on productivity and automation use cases
- Priority areas: email management, calendar, task tracking
- Active integrations: Telegram, Slack (update as configured)

## Security & Privacy Infrastructure
- **PII redaction:** Automated layer catches personal emails, phone
  numbers, dollar amounts. Wired into notification and delivery paths.
- **Data classification tiers:** Confidential (DM-only), Internal
  (group chats OK), Restricted (external only with approval).
- **Content gates:** Frontier scanner for outbound emails and
  security-sensitive operations.
- **Secret handling:** Never share credentials unless explicitly
  requested by name with confirmed destination.

## Analysis Patterns
- When the user asks about a recommendation in conversation, pull
  the data locally and include it in the reply. Don't re-post to
  messaging (creates duplicate messages).
- When discussing config changes, just make the fix. Skip the
  accounting of alternative approaches unless asked.

## LLM Usage Queries
- Query the interactions database at ~/workspace/data/interactions.db
- Use the llm_calls table for model usage and cost tracking

## Operational Lessons
- **Duplicate delivery prevention:** Content already posted is
  delivered. Don't re-send it. Address follow-up questions instead.
- **Lock files:** Check for stale lock files if ingestion hangs.
  Delete if the owning PID is dead.
- **Gateway token sync:** Multiple locations store the gateway token.
  After updates, verify they match.
- **Notification validation:** Always validate API responses, not
  just CLI exit codes. Silent failures happen.
- **Model routing:** All LLM calls route through a centralized router
  with comprehensive logging.

## Email Triage Patterns
- **High priority:** Meetings, partner communications, payments,
  tax documents, family/school, bills
- **Medium:** Inbound leads, guest bookings, shipping
- **Low:** Newsletters, social notifications, marketing

## System Health & Monitoring
- Consolidated health check runs during heartbeats
- Persistent failure tracking alerts on repeated failures
- Notification batching reduces noise
- Tiered testing (unit, integration, E2E)

---
*Specific task logs are moved to daily memory files to keep this
file concise.*
