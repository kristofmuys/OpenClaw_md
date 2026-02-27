# Prompt 19: Data Classification and Privacy Controls

**What this builds:** Access control enforced through the system prompt.

```
Implement data classification and context-aware privacy for your agent:

1. Define three data tiers in your AGENTS.md:
   - Confidential (private/DM only): financial figures, CRM contact details,
     deal values, daily notes, personal email addresses
   - Internal (group chats OK, no external): strategic notes, analysis outputs,
     tool results, task data, system health info
   - Restricted (external only with explicit approval): general knowledge
     responses. Everything else requires you to say "share this" before
     it leaves internal channels.

2. Context-aware gating rules (also in AGENTS.md):
   - The agent checks message metadata for context type (DM vs group vs channel)
   - In non-private contexts, it automatically:
     * Skips reading daily notes (contain personal details)
     * Skips CRM queries that return contact details
     * Skips financial data, deal values, dollar amounts
     * Skips personal email addresses (work emails are fine)
   - When context type is ambiguous, default to the more restrictive tier

3. Conditional file loading:
   - MEMORY.md (contains preferences, strategic notes, personal details):
     only loaded in private conversations with you, never in group contexts
   - This single config decision prevents the most common personal data leak

4. Identity separation:
   - Work contact info (company email) goes in USER.md (loaded everywhere)
   - Personal contact info (personal email, phone) goes in MEMORY.md
     (private chats only)

5. Outbound redaction as a safety net:
   - PII redaction module catches personal emails, phone numbers, dollar
     amounts in outbound messages
   - Work-domain emails pass through since they're safe in work contexts
   - This catches anything the classification rules miss
```
