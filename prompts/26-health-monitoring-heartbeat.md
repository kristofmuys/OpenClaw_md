# Prompt 26: Health Monitoring Heartbeat

**What this builds:** A health monitoring heartbeat system with tiered checks.

```
Add a health monitoring heartbeat system:

1. Daily checks:
   - Verify social media tracker data is fresh (flag if older than 3 days)
   - Check git repo size (alert if over 500MB, signals binary blob accumulation)
   - Scan error logs for recurring issues
   - Run a git backup of all workspace changes
   - Verify all expected cron jobs ran successfully

2. Weekly checks:
   - Verify the gateway only binds to localhost (not exposed to the internet)
   - Verify authentication is enabled and token is non-empty
   - Check for outdated dependencies (npm audit, etc.)
   - Verify backup integrity (download and decrypt latest backup)

3. Monthly checks:
   - Scan memory files for suspicious patterns (potential prompt injection)
   - Review and clean up stale cron jobs
   - Security audit of workspace files
   - Review model usage costs and optimize if needed

4. Philosophy:
   - Only alert when something needs attention
   - If the heartbeat system is silent, everything is fine
   - Track all check timestamps in heartbeat-state.json
   - Checks don't re-run unnecessarily (use timestamps to gate)

5. State file (memory/heartbeat-state.json):
   - Track last check time for each check type
   - Track alert frequency to implement exponential backoff
   - Reset state if file is corrupted (with user notification)
```
