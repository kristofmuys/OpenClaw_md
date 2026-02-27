# Prompt 4: Business Advisory Council

**What this builds:** Parallel independent AI expert analysis with synthesis and feedback loops.

```
Build a business analysis system with parallel independent AI experts:

1. Data collectors (one per source):
   - YouTube analytics, Instagram engagement, X/Twitter analytics
   - CRM contacts, email activity, meeting transcripts
   - Cron job reliability, Slack messages, task manager data
   - Newsletter stats, deal pipeline data

2. Specialist personas (run in parallel, isolated from each other):
   - RevenueGuardian: revenue trends, burn rate, cash position
   - GrowthStrategist: audience growth, content performance
   - SkepticalOperator: what could go wrong, risks
   - InnovationScout: opportunities, automation ideas
   - ContentAnalyst: content strategy, engagement patterns
   - RelationshipManager: CRM health, key contacts
   - TechDebtWatcher: code quality, test coverage, dependencies
   - SecurityReviewer: security posture, vulnerabilities

3. Synthesis layer:
   - Merge findings from all experts
   - Eliminate duplicates
   - Rank recommendations by priority and impact
   - Deliver numbered digest to Telegram

4. Interaction:
   - "Tell me more about #3" triggers a deeper dive on that recommendation
   - Approve/reject feedback loop: system learns your preferences over time
   - Weekly digest with trend analysis vs. previous week

5. Data freshness:
   - Each collector tracks its own last-sync timestamp
   - Alert if any data source is stale (>3 days)
   - Run collectors in parallel to minimize total runtime
```
