# Prompt 6: Social Media Tracking

**What this builds:** Daily snapshots of social media performance across platforms.

```
Build a social media tracker:

1. Data collection (daily snapshots):
   - YouTube: per-video views, watch time, engagement, subscriber conversion
   - Instagram: per-post engagement, account growth, story metrics
   - X/Twitter: per-post impressions, likes, retweets, bookmarks, follower gains
   - TikTok: follower growth, video performance

2. Storage:
   - SQLite databases per platform (WAL mode)
   - Append-only snapshots with timestamps
   - Deduplication to avoid double-counting

3. Daily briefing integration:
   - Yesterday's performance across all platforms
   - Outliers: what performed unusually well or poorly
   - Week-over-week trends

4. Business council integration:
   - Feed all data into the advisory council for cross-platform analysis
   - Correlate content performance with posting time, format, topic

5. Alerts:
   - Unusual drops in engagement (>20% below 7-day average)
   - Viral content (>5x normal engagement)
   - Follower milestone notifications
```
