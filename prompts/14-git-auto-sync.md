# Prompt 14: Git Auto-Sync

**What this builds:** Hourly git auto-sync with conflict detection and sensitive data protection.

```
Set up hourly git auto-sync:

1. Core sync (run hourly via cron):
   - Auto-commit all workspace changes
   - Pull before push to handle merge conflicts
   - PID file guard prevents concurrent sync runs
   - Tag each sync with a timestamp in the commit message

2. Conflict handling:
   - Detect merge conflicts
   - Notify user via Telegram instead of forcing a resolution
   - Include conflict details in the notification
   - Pause sync until conflict is resolved

3. Pre-commit safety:
   - Check for accidentally staged sensitive files
   - Block commits containing: .env files, browser profile cookies, session tokens
   - Check for large binary files (>10MB) that shouldn't be in git
   - Alert if repo size exceeds threshold (500MB)

4. Failure handling:
   - Alert on persistent push failures (3+ consecutive failures)
   - Log all sync attempts to cron-log database
   - Include error details in failure notifications

5. Status:
   - "git status" command shows last sync time and any pending changes
   - Weekly report: sync reliability, average commit size, any issues
```
