# Prompt 25: Asana Integration

**What this builds:** Asana integration for project management and task tracking.

```
Connect your AI assistant to Asana:

1. Core operations:
   - Create tasks in specified projects
   - Update task status, assignee, due date
   - Add comments to existing tasks (never edit descriptions)
   - List tasks by project, assignee, or due date
   - Search tasks by keyword

2. Video idea pipeline integration:
   - When a video idea is approved, create a structured Asana card
   - Fields: idea title, description, research findings, sources, angles
   - Post completion message with Asana link back in Slack thread

3. Update rule:
   - Add new information as comments, not by editing the description
   - This preserves history and prevents data loss
   - Exception: fix typos or factual errors in descriptions

4. Sync:
   - Cache task data locally in SQLite for fast queries
   - Sync on demand or on a schedule
   - Feed task status into business advisory council

5. Natural language interface:
   - "Create a task in Video Pipeline: [description]"
   - "What's in my Asana backlog?"
   - "Mark task #123 as complete"
   - "Show me overdue tasks"
```
