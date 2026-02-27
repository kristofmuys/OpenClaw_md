# HEARTBEAT.md

Keep this short. It runs every hour.

## Every heartbeat
- Update memory/heartbeat-state.json timestamps for checks performed
- Git backup: run auto-git-sync. If it exits non-zero, log a warning.
  Alert Kris only for real breakages (merge conflicts, persistent push failures).
- System health check (with --notify so critical issues route with priority)
- Cron failure deltas (with --notify)
- Persistent failure check (with --notify)

## Once daily
- Repo size check (alert if git repo exceeds 500MB)
- Error log scan for recurring issues

## Weekly
- Verify gateway is bound to loopback only
- Verify gateway auth is enabled and token is non-empty

## Reporting
Heartbeat turns should usually end with NO_REPLY.
Only send a direct heartbeat message when the notifier path itself is
broken and Kris needs intervention.

If memory/heartbeat-state.json is corrupted, replace it with:
{"lastChecks": {"errorLog": null, "securityAudit": null, "lastDailyChecks": null}}
Then alert Kris.
