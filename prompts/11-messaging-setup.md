# Prompt 11: Messaging Setup

**What this builds:** Organized Telegram topics and Slack integration with strict routing rules.

```
Set up messaging channels for your AI assistant:

1. Telegram topics (create these in your group):
   - Daily Brief: morning briefing (cron-owned, respond to follow-ups only)
   - Personal CRM: contact queries and follow-up nudges
   - Email: email-related queries and draft proposals
   - Knowledge Base: KB ingestion and querying notifications
   - Meta-Analysis: business advisory council digests
   - Video Ideas: video pitch discussion and feedback
   - Earnings: financial tracking and earnings reports
   - Cron Updates: automated job notifications (failures only)
   - Financials: financial data (locked down, owner only)
   - Health: food logging and health tracking
   - Self-Improvement: agent self-improvement and debugging

2. Routing rules:
   - Each topic gets exactly its content type. No cross-posting.
   - When sending files, send the actual file, not a link.
   - Cron Updates: failures only. Success is silent.
   - Financials: never share outside DM or this topic.

3. Slack integration:
   - Mention-only mode: only respond when directly mentioned
   - User allowlist: only authorized users can invoke the bot
   - Auto-reaction on receipt: eyes emoji (👀) so user knows it saw the message
   - Response style: one complete message, no intermediate "thinking..." messages

4. Communication style:
   - Two messages max per task: acknowledgment, then result
   - No play-by-play narration of what you're doing
   - Brief acknowledgment if task will take time, then one complete result
   - In group chats: sharp colleague mode, not friend mode
```
