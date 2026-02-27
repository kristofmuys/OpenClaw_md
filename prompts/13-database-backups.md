# Prompt 13: Database Backups

**What this builds:** Automated encrypted database backup system with restore capability.

```
Set up an automated database backup system:

1. Discovery and backup (run hourly):
   - Auto-discover all SQLite databases in the project (no manual config)
   - New databases get picked up automatically
   - Also back up JSONL event logs
   - Create a manifest file mapping each file to its original absolute path

2. Encryption and upload:
   - Encrypt before uploading (GPG or similar)
   - Upload to cloud storage (Google Drive, S3, etc.)
   - Keep last 7 backups (configurable)
   - Alert immediately via Telegram if backup fails

3. Restore script:
   - Download latest backup from cloud storage
   - Read the manifest for original file paths
   - Restore each database to its original location
   - Support preview/list mode and force mode

4. Integrity drill (run weekly):
   - Validate: download works, decryption works, manifest parses correctly, checksums match
   - Runs without modifying the current filesystem
   - Catches backup corruption before you need to restore
   - Report results to self-improvement channel

5. Monitoring:
   - Track backup size over time (alert if growing unusually fast)
   - Verify backup freshness (alert if last successful backup >2 hours old)
```
