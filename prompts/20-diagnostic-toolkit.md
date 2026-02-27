# Prompt 20: Diagnostic Toolkit

**What this builds:** Health check scripts, cron job debugging tools, and log analysis utilities.

```
Build a diagnostic toolkit for your agent:

1. System health check script:
   - Check if the agent server/gateway process is running
   - Check if the expected port is reachable
   - Query your interaction store for recent API/LLM failure rates
   - Scan structured event logs for recent errors
   - Scan server/gateway error logs
   - Output a pass/fail summary with details on failures
   - State file to track alert frequency (exponential backoff so you
     don't get spammed with the same alert)

2. Cron job debugging tools:
   - Query tool: filter cron history by job name, status (success/failure),
     date range, with configurable result limit
   - Persistent failure detector: flag when the same job has failed 3+ times
     within a 6-hour window (distinguishes flaky jobs from one-off failures)
   - Stale job cleaner: auto-mark jobs stuck in "running" state for >2 hours
     as failed (handles machine sleep, process crashes)

3. Unified log viewer:
   - Single CLI that reads from your unified event log stream
   - Filter by: event name, log level, content substring, time range
   - JSON output mode for piping into other tools
   - Quick-access aliases for common queries (e.g., "errors in the last hour")

4. Model/provider diagnostics:
   - Status command: show which model is actually running, context usage,
     fallback chain status, plugin connections
   - Canary test: send a test prompt and verify response metadata matches
     the expected provider (catches silent auth failures)
   - Usage dashboard: model costs, cron reliability, storage sizes, API
     call counts, all from one command
```
