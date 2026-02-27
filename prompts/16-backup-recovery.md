# Prompt 16: Backup and Recovery

**What this builds:** Automated encrypted backups, git sync, restore scripts, and integrity verification.

```
Build backup and recovery for your agent workspace:

1. Database backup (run hourly or on your preferred schedule):
   - Auto-discover all .db/.sqlite files across the workspace
   - Also back up JSONL event logs
   - Create a manifest file mapping each file to its original absolute path
   - Encrypt before uploading to cloud storage (GPG or similar)
   - Upload to your cloud storage (Google Drive, S3, etc.)
   - Keep a configurable number of recent backups (e.g., last 7)

2. Git sync (hourly):
   - Auto-commit workspace changes
   - Pull before push to handle merge conflicts
   - PID file guard prevents concurrent sync runs
   - Alert on failure via your messaging platform

3. Restore script:
   - Download latest backup from cloud storage
   - Read the manifest for original file paths
   - Restore each database to its original location
   - Support a preview/list mode and a force mode

4. Integrity drill:
   - Periodic script that validates: download works, decryption works,
     manifest parses correctly, checksums match
   - Runs without modifying the current filesystem
   - Catches backup corruption before you need to restore
```
