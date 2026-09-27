---
name: notebooklm-query
description: Ask grounded questions against a consumer NotebookLM notebook and report citations when available. Prefer MCP ask/query tools; browser fallback for interactive chat on notebooklm.google.com. Optional Studio artifacts only if supported.
---

# NotebookLM query

Use this skill for grounded Q&A against an existing consumer NotebookLM notebook.

## Prefer MCP when connected

1. Confirm the NotebookLM MCP is connected (setup skill). Use **exact** tool names from the server.
2. Resolve the notebook: list notebooks via MCP, or use an ID/URL the **user supplied** or a **prior tool result**. Never invent notebook IDs.
3. Call the MCP ask/query tool exposed by the server (typical illustration only: something like `notebook_ask` -- verify the real name).
4. Return the answer and **citations / source excerpts when the tool provides them**.
5. Studio artifacts (audio overview, video, report, etc.): only invoke generators the connected MCP or UI actually exposes; do not invent artifact types or claim support that is not present.
6. Never print cookies or tokens.

## Browser fallback

If MCP is unavailable:

1. Open the notebook on https://notebooklm.google.com.
2. Use the in-notebook chat / discussion panel to ask the question.
3. Copy the answer and any visible citation chips/links back to the user.
4. For Studio outputs, use the Studio panel in the UI only when the user asks and the UI offers that artifact.

## Guardrails

- Answers should stay grounded in notebook sources; say when the product refuses or has no sources.
- Consumer product only -- not Google Cloud NotebookLM Enterprise.
- Do not invent model names, citation IDs, or tool slugs.
