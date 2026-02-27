# Prompt 23: Migrate to the Claude Agents SDK (OAuth)

**What this builds:** A unified LLM router that authenticates with Anthropic via OAuth instead of static API keys.

```
Build a unified LLM routing layer using the Anthropic Claude Agent SDK
with OAuth authentication instead of static API keys. It should support
multiple providers, log every call to SQLite, and estimate costs.

Create these modules in a shared/ directory (Node.js):

1. MODEL UTILITIES (shared/model-utils.js)

   - Map of friendly aliases to official model names
     (e.g., "sonnet-4" -> "claude-sonnet-4-5", "haiku-4" -> "claude-haiku-4-5")
   - isAnthropicModel(model): true if model name contains claude/opus/sonnet/haiku
   - normalizeAnthropicModel(model): resolve aliases, strip provider prefixes
   - detectModelProvider(model): return "anthropic", "openai", or null

2. CALL LOGGER (shared/interaction-store.js)

   SQLite database (WAL mode) with an llm_calls table:
   id, timestamp, provider, model, caller, prompt, response,
   input_tokens, output_tokens, cost_estimate, duration_ms, ok, error

   - logLlmCall(): fire-and-forget insert. Truncate prompt/response to 10K
     chars. Redact anything that looks like an API key or bearer token
     before storing.
   - estimateTokensFromChars(): rough estimate at ~4 chars per token
   - Pricing table for cost estimation (USD per 1M tokens per model)

3. ANTHROPIC SDK WRAPPER (shared/anthropic-agent-sdk.js)

   Wraps @anthropic-ai/claude-agent-sdk with OAuth tokens.

   OAuth token resolution:
   - Check CLAUDE_CODE_OAUTH_TOKEN env var first
   - Fall back to parsing it from your .env file
   - If ANTHROPIC_API_KEY is also set, throw an error (they conflict
     in OAuth-only mode)

   Startup smoke test (runs once per process on first call):
   - Send "Reply with exactly AUTH_OK and nothing else."
   - Validate response contains AUTH_OK
   - If it fails, throw a clear error that credentials are bad
   - 20-second timeout, can be disabled via env var

   Main function: runAnthropicAgentPrompt({ model, prompt, timeoutMs,
   caller, maxTurns, skipLog })
   - Run smoke test before first real request
   - Call the SDK's query() in toolless mode (tools: [], maxTurns: 1)
   - Stream response messages, extract text from content blocks
   - Handle timeouts via AbortController
   - Log success/failure to interaction store
   - Return { text, provider: "anthropic" }

4. UNIFIED ROUTER (shared/llm-router.js)

   Single entry point for all LLM calls:

   runLlm(prompt, { model, timeoutMs, caller, skipLog })
   - If isAnthropicModel(model): route to the Anthropic SDK wrapper
   - Otherwise: route to your OpenAI/other provider handler
   - Return { text, durationMs }

   Callers never think about which provider to use. They just pass a
   model name and get text back.

SETUP:

   npm install @anthropic-ai/claude-agent-sdk
   Run "claude login" to get your OAuth token
   Add to .env: CLAUDE_CODE_OAUTH_TOKEN=<your-token>
   Remove ANTHROPIC_API_KEY if it exists

USAGE:

   const { runLlm } = require('./shared/llm-router');
   const result = await runLlm("Your prompt", {
     model: "claude-sonnet-4-5",
     caller: "my-script",
   });
   console.log(result.text);
```
