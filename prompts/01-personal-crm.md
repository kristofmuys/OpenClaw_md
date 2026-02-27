# Prompt 1: Personal CRM

**What this builds:** A personal CRM with auto-discovery from email/calendar, semantic search, relationship scoring, follow-ups, and email draft generation.

```
Build a personal CRM with these components:

1. Contact discovery pipeline:
   - Scan your email (Gmail API or similar) and calendar for contacts
   - Filter out: newsletters, noreply senders, large meetings (>10 people),
     internal/company domains
   - Implement a learning system: build skip patterns from approve/reject decisions
   - After enough decisions (~50), suggest switching to auto-add mode

2. Database (SQLite, WAL mode):
   - contacts: name, email, company, role, priority, relationship_score
   - interactions: meetings, emails, calls with timestamps
   - follow_ups: due dates, snoozing, status tracking
   - contact_context: timeline entries with vector embeddings (768-dim)
   - contact_summaries: LLM-generated relationship summaries
   - meetings: synced from your meeting recorder (transcript, summary, attendees)
   - meeting_action_items: with assignee, ownership flag, task app link
   - company_news: high-signal news items per company

3. Natural language interface:
   - Intent detector supporting query types like:
     "Tell me about [name]", "Who at [company]?", "Follow up with [name] in 2 weeks",
     "Who needs attention?", "Stats"
   - Semantic search over contact_context embeddings
   - Integration with your messaging platform for queries and notifications

4. Relationship intelligence:
   - Relationship scorer (0-100 based on recency, frequency, priority)
   - Nudge generator for contacts needing attention
   - Relationship profiler (type, communication style, key topics)

5. Daily cron job:
   - Scan last 24h of email/calendar activity
   - Add new contacts, extract context for existing ones
   - Update relationship summaries
   - Report results to your updates channel

6. Email draft system:
   - Thread lookup via email API
   - Feed CRM context + meeting context to LLM for draft generation
   - Two-phase approval: proposed -> approved -> draft created in email client
   - Safety gate: draft creation must be explicitly enabled via config flag
```
