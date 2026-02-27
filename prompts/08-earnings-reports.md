# Prompt 8: Earnings Reports

**What this builds:** Automated earnings report system with dynamic scheduling.

```
Build an earnings report system:

1. Weekly preview (Sunday 9am):
   - Preview upcoming earnings for stocks on your watchlist
   - Include: company, expected date/time, analyst consensus, key metrics to watch

2. Dynamic scheduling:
   - Let user pick which tickers to cover
   - Create one-time cron jobs timed to run right after earnings release
   - Jobs auto-delete after running (deleteAfterRun: true)

3. Report format (narrative, not tables):
   - Overall verdict: beat or miss, by how much
   - Market reaction: how the stock moved after-hours
   - 2-3 most interesting takeaways (guidance, surprises, management commentary)
   - Keep it narrative, not a wall of numbers

4. Delivery:
   - Reports go to the Earnings Telegram topic
   - Include ticker symbol and company name in subject
   - Link to earnings call transcript if available

5. Watchlist management:
   - Add/remove tickers via natural language ("add NVDA to earnings watchlist")
   - Show current watchlist on request
   - Persist watchlist in a simple JSON file
```
