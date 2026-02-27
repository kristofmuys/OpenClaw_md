# Prompt 2: Meeting Intelligence

**What this builds:** Integration with a meeting recording tool for automatic CRM updates, insight extraction, and action item tracking.

```
Build a meeting recording integration (e.g., Fathom, Otter, Fireflies):

1. API client for your meeting recorder (meetings, transcripts, summaries, action items)

2. Calendar-aware polling:
   - Run on a short interval during business hours (e.g., every 5 min, 7am-5pm)
   - Check today's calendar for meetings with external attendees
   - Only poll the meeting recorder after meeting end + buffer (e.g., 20 minutes)
   - Track last handled time to avoid duplicate processing
   - This prevents wasted API calls during non-meeting hours.

3. Meeting processing:
   - Match attendees to CRM contacts by email
   - Extract relationship insights using an LLM
   - Create context entries with vector embeddings
   - Refresh relationship summaries for attendees

4. Action item pipeline:
   - Extract action items from transcript
   - Verify ownership (is this my action item or someone else's?)
   - Send approval queue to your messaging platform
   - On approval, create a task in your task manager (Todoist, Linear, etc.)

5. Two modes:
   - Polling mode: fetch new meetings since last poll (for cron)
   - Backfill mode: pull historical meetings (e.g., last 90 days)
```
