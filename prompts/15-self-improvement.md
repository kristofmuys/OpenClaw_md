# Prompt 15: Self-Improvement

**What this builds:** Error capture, automated review councils, tiered testing, and proactive error reporting.

```
Build self-improvement systems for your agent:

1. Learnings directory:
   - LEARNINGS.md: captured corrections and insights from user feedback
   - ERRORS.md: recurring error patterns the agent has encountered
   - FEATURE_REQUESTS.md: ideas for improvement
   - Optional: post-tool-use hook that scans tool output for error patterns

2. Automated review councils (daily cron jobs):
   - Platform health review: cron reliability, code quality, test coverage,
     prompt quality, storage usage, data integrity
   - Security review: multi-perspective analysis (offensive, defensive,
     data privacy, operational realism)
   - Innovation scout: scan codebase for automation opportunities,
     propose ideas with accept/reject feedback loop

3. Tiered testing:
   - Tier 1 (nightly, free): integration tests, no LLM calls
   - Tier 2 (weekly, low cost): tests that make live LLM calls
   - Tier 3 (weekly, moderate cost): full end-to-end tests including
     messaging platform round-trips

4. Error reporting rule (add to your agent's system prompt):
   - Proactively report all failures via your messaging platform
   - Include error details and context
   - The user can't see stderr or background logs, so proactive reporting
     is the only way they'll know something went wrong
```
