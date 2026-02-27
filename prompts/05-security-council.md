# Prompt 5: Security Council

**What this builds:** Automated nightly security review with multi-perspective AI analysis.

```
Create an automated nightly security review:

1. Schedule: Run at 3:30am (your local time) to avoid peak usage hours

2. Analysis perspectives (run in parallel):
   - Offensive: what could an attacker exploit?
   - Defensive: are protections adequate?
   - Data privacy: is sensitive data handled correctly?
   - Operational realism: are security measures practical or just theater?

3. What to analyze:
   - Entire codebase (AI reads through actual code, not just static rules)
   - Configuration files (.env handling, secrets management)
   - Network exposure (gateway binding, open ports)
   - Skill permissions and third-party dependencies
   - Memory files for suspicious patterns (potential prompt injection)

4. Output:
   - Structured report with numbered findings
   - Severity levels: Critical, High, Medium, Low
   - Critical findings alert immediately via Telegram
   - Full report delivered to self-improvement channel

5. Interaction:
   - "Tell me more about finding #3" triggers deeper analysis
   - Accept/dismiss findings with feedback loop
   - Monthly trend report: are we getting more or less secure?
```
