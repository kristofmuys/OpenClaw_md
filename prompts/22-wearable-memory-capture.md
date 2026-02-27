# Prompt 22: Wearable Memory Capture

**What this builds:** A wearable transcription system that captures conversations to daily files.

```
Build a wearable memory capture system (e.g., using a recording pendant,
smart glasses, or any continuous transcription device):

1. Stream handler:
   - Connect to your device's transcription stream/API
   - Parse incoming transcriptions into structured entries
   - Save to daily markdown files (memory/YYYY-MM-DD.md)
   - Tag entries by type: conversation, fact, todo, voice-memo

2. Backup poll (e.g., every 10 minutes):
   - Fetch any transcriptions the stream handler missed
   - Deduplicate against already-saved entries
   - Append to the same daily markdown files

3. Search interface:
   - Natural language queries via your messaging platform or CLI
   - LLM searches memory files for relevant context
   - Returns answers grounded in actual transcripts with timestamps
   - Example queries: "What was I talking about at lunch?",
     "Did someone mention a deadline?", "What restaurant was recommended?"

4. Privacy:
   - Daily notes are Confidential tier (private chats only)
   - Never loaded in group chat contexts
   - Same data classification as your main memory system
   - Consider local-only storage (no cloud sync) for maximum privacy
```
