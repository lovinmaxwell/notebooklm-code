---
name: notebooklm-sources
description: Create or list NotebookLM notebooks and add URL, text, or file sources; check ingestion. Prefer connected NotebookLM MCP tools; otherwise use the browser on notebooklm.google.com. Never invent notebook IDs.
---

# NotebookLM sources

Use this skill to manage consumer NotebookLM notebooks and sources.

## Prefer MCP when connected

1. Discover available tools from the connected NotebookLM MCP (setup skill). Use the **exact** tool names returned -- do not invent slugs.
2. Typical illustrations only (names vary by package/version): list/create notebooks; add URL, pasted text, or file sources; list sources; check status.
3. **Never invent notebook IDs or source IDs.** Only use IDs returned by tools or supplied by the user.
4. After adding a source, wait for or poll ingestion/status using whatever the MCP exposes; report success/failure clearly.
5. Do not print cookies, tokens, or raw auth state.

## Browser fallback

If MCP is unavailable:

1. Open https://notebooklm.google.com (consumer UI; may also appear as Gemini Notebook branding).
2. Create or open a notebook in the UI.
3. Add sources via the product UI (Upload, Link, Paste text, etc.).
4. Wait until the UI shows the source as ready before querying.
5. Ask the user for any notebook URL or ID visible in the address bar / UI if later MCP use needs it -- do not fabricate IDs.

## Guardrails

- Consumer notebooklm.google.com only -- not NotebookLM Enterprise.
- No secrets in chat logs.
- If a tool fails, surface the error; do not retry with guessed parameters or invented IDs.
