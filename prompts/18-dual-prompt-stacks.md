# Prompt 18: Dual Prompt Stacks with Sync

**What this builds:** Two parallel prompt configurations optimized for different model families.

```
Set up dual prompt stacks for multi-model support:

1. Primary stack (Claude-optimized):
   - Natural language style, explain the "why" behind rules
   - Avoid aggressive emphasis (ALL-CAPS, excessive "CRITICAL", "MUST")
   - These models overtrigger on urgency markers

2. Secondary stack in a separate directory (GPT-optimized):
   - XML tags or structured markers for hierarchy
   - ALL-CAPS emphasis works well here
   - More explicit structural formatting

3. Both stacks must contain identical operational facts:
   - Same channel IDs, project IDs, file paths
   - Same security rules, data classification, cron standards
   - Same learned preferences and workflow triggers
   Only the formatting and style should differ.

4. Automated sync review script (run nightly):
   - Compare both stacks for file coverage (every file in one should exist
     in the other)
   - Diff operational facts between matching files (channel IDs, rules, paths)
   - Report discrepancies to your monitoring/self-improvement channel
   - This catches "I updated the Telegram topic ID in the Claude prompts
     but forgot the GPT prompts" class of bugs

5. Model swap procedure:
   - Update your framework config to point to the new model
   - Restart the gateway/server
   - Verify with a canary message: send a structured test prompt and check
     response metadata to confirm the correct provider is responding
   - If metadata shows the wrong provider, auth failed and fallback kicked in
```
