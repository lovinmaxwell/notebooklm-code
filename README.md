# NotebookLM Code

A Cursor plugin for working with **consumer** Google NotebookLM ([notebooklm.google.com](https://notebooklm.google.com)) from Cursor or Grok Bot agents: community MCP setup, notebook/source management, and grounded Q&A with citations.

> **Important:** There is **no official public consumer NotebookLM API** and **no official CLI**. This plugin does **not** talk to Google Cloud NotebookLM Enterprise / Composio enterprise products. Integration is via (1) a community MCP server that uses Google **session** auth (unofficial / reverse-engineered), and (2) a browser fallback on notebooklm.google.com.

## Prerequisites

- Node.js ≥ 18 (for the recommended MCP via `npx`).
- A personal Google account that can sign in to [notebooklm.google.com](https://notebooklm.google.com).
- Cursor with MCP enabled (`~/.cursor/mcp.json`), **or** willingness to use the browser fallback skill guidance.
- Prefer a **dedicated** Google account for automation; session cookies are sensitive — never print them.

## Recommended MCP (primary)

**[@roomi-fields/notebooklm-mcp](https://github.com/roomi-fields/notebooklm-mcp)** (`npx -y @roomi-fields/notebooklm-mcp`) — maintained open-source MCP + REST bridge for consumer NotebookLM (citation Q&A, sources, Studio artifacts). Auth is session-based; not an official Google API.

### Wire into Cursor

Add to `~/.cursor/mcp.json` (merge with any existing `mcpServers`):

```json
{
  "mcpServers": {
    "notebooklm": {
      "command": "npx",
      "args": ["-y", "@roomi-fields/notebooklm-mcp"]
    }
  }
}
```

Then complete one-time Google login in a **terminal** (not via the agent), so a visible browser can open:

```bash
npx -y -p @roomi-fields/notebooklm-mcp notebooklm-mcp-setup-auth
```

Reload Cursor / restart MCP, then confirm NotebookLM tools appear in the MCP tool list. Use the **exact tool names** exposed by the connected server — do not invent slugs.

### Alternatives (brief)

- [PleasePrompto/notebooklm-mcp](https://github.com/PleasePrompto/notebooklm-mcp) — retrieval-focused MCP (`npx notebooklm-mcp@latest`).
- [jacob-bd/gemini-notebook-mcp-cli](https://github.com/jacob-bd/gemini-notebook-mcp-cli) (`notebooklm-mcp-cli` / `nlm`) — CLI + MCP with client setup helpers.
- Others in the ecosystem (e.g. Cezial/notebooklm-mcp-server, amp-rh/notebooklm-agent-plugin, WillWetzel/notebooklm-mcp-2026) — evaluate before installing; pick **one** server to avoid overlapping tool names.

## Install for local testing

1. Copy this directory to:

   ```text
   ~/.cursor/plugins/local/notebooklm-code
   ```

2. Reload Cursor with **Developer: Reload Window**.
3. Confirm the skills appear in Customize settings.
4. Wire MCP as above (Grok Bot only installs **marketplace** plugins; skills still help when MCP is already in `~/.cursor/mcp.json`).

## Use from chat

Examples:

> Set up the NotebookLM MCP for Cursor and verify the tools show up.

> Create a notebook, add https://example.com/docs as a source, and confirm ingestion finished.

> Ask my NotebookLM notebook &lt;id-from-list-or-user&gt;: What are the three main claims? Include citations.

Skills: `notebooklm-setup`, `notebooklm-sources`, `notebooklm-query`. If MCP is unavailable, follow the browser fallback on https://notebooklm.google.com.

## Publishing

Cursor marketplace: <https://cursor.com/marketplace/publish>.
