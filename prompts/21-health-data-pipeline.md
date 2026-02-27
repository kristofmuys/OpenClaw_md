# Prompt 21: Health Data Pipeline

**What this builds:** A pipeline pulling biometric data from wearables into a unified timeline.

```
Build a health data pipeline:

1. Connector scripts (one per data source):
   - Wearable ring API (e.g., Oura): sleep stages, HRV, readiness, activity
   - Phone health exports (e.g., Apple Health CSV): steps, heart rate, workouts
   - Smart scale API (e.g., Withings): weight, body composition
   Each connector normalizes to a common JSONL format:
   {timestamp, source, metric, value, unit}

2. Unified timeline:
   - Append-only JSONL file (health-timeline.jsonl)
   - One line per measurement
   - All sources write to the same file

3. Morning cron job:
   - Pull latest data from all configured sources
   - Run LLM analysis on recent timeline entries
   - Generate: daily health summary, trend flags, coaching tips
   - Deliver to your health/wellness channel

4. Trend analysis:
   - Look back over weeks/months for patterns
   - Flag: poor sleep streaks, HRV drops, weight changes
   - Cross-reference: sleep quality vs activity level, weight vs nutrition
```
