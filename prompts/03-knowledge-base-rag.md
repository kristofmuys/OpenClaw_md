# Prompt 3: Knowledge Base (RAG System)

**What this builds:** A RAG knowledge base for ingesting web content, documents, and social posts, with semantic search and content sanitization.

```
Build a knowledge base with RAG (Retrieval-Augmented Generation):

1. Ingestion pipeline:
   - Support multiple source types: URLs (web articles), YouTube videos (pull transcript),
     X/Twitter posts (follow full threads), PDFs, and plain text
   - When a tweet links to an article, ingest both the tweet and the full article
   - Extract key entities (people, companies, concepts) from each source
   - Store everything in SQLite with vector embeddings (768-dim)
   - For paywalled sites you're logged into, use browser automation through your Chrome session

2. Content sanitization:
   - Strip tracking parameters from URLs
   - Normalize whitespace and encoding
   - Remove boilerplate (nav, footer, ads) from web pages
   - Sanitize against prompt injection patterns in ingested content

3. Search interface:
   - Natural language queries with semantic search
   - Time-aware ranking (recent sources rank higher)
   - Source-weighted ranking (prefer primary sources)
   - Return results with source attribution and timestamps

4. Cross-posting:
   - Optionally cross-post summaries to a Slack channel with attribution
   - Tag-based routing: different tags route to different channels

5. Cron job:
   - Daily ingestion of bookmarked/queued URLs
   - Deduplication against already-ingested content
   - Report new ingestions to your knowledge base channel
```
