# Prompt 24: Model Usage and Cost Tracking

**What this builds:** A model usage tracker that logs every AI API call across all providers.

```
Build a model usage tracker:

1. Logging (every API call):
   - Provider (Anthropic, OpenAI, Google, xAI)
   - Model name
   - Input/output token counts
   - Task type (cron, user request, subagent, etc.)
   - Estimated cost per call
   - Duration in milliseconds
   - Success/failure status

2. Storage:
   - SQLite database (WAL mode)
   - JSONL backup for portability
   - Redact prompt/response content to 10K chars max
   - Redact API keys and bearer tokens before storing

3. Reports:
   - Daily cost summary by model and task type
   - Weekly trend: are costs going up or down?
   - Monthly breakdown with top cost drivers
   - Alert if daily cost exceeds threshold

4. Query interface:
   - "How much did I spend on AI this week?"
   - "Which model am I using most?"
   - "What's my most expensive cron job?"
   - Natural language queries via messaging platform

5. Integration:
   - Feed data into business advisory council
   - Include in daily briefing if costs are unusual
   - Alert immediately if a single call costs >$1 (likely a bug)
```
