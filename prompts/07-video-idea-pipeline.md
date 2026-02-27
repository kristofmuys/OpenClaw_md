# Prompt 7: Video Idea Pipeline

**What this builds:** Automated video idea research and tracking triggered by Slack mentions.

```
Create a video idea pipeline:

1. Trigger:
   - Slack mention + "potential video idea" + description
   - Read the full Slack thread for context

2. Research phase (run in parallel):
   - X/Twitter research: what are people saying, what angles exist
   - Knowledge base query: related articles and content already saved
   - Semantic similarity check against all previous pitches
   - If similarity > 40%, skip and report the duplicate

3. Output:
   - Structured task card in your project manager (Asana, Linear, etc.)
   - Fields: idea title, description, research findings, relevant sources, suggested angles
   - Post completion message with task link back in the Slack thread

4. Pitch tracking:
   - Status tracking: pitched, accepted, rejected, produced, duplicate
   - Learn from feedback: what types of ideas get accepted vs. rejected
   - Weekly report: pipeline health, acceptance rate, ideas in progress

5. Dedup system:
   - Vector embeddings for all pitches
   - Similarity threshold: 40% triggers duplicate flag
   - Show the similar pitch when flagging so you can decide
```
