---
name: notebooklm-setup
description: Install and configure a community NotebookLM MCP for consumer notebooklm.google.com, complete Google session auth, and verify tools appear. Use when MCP is missing, auth fails, or before first NotebookLM use from an agent.
---

# NotebookLM setup

Use this skill before the first NotebookLM task, or whenever the community MCP is missing or authentication fails.

## Scope (read first)

- Targets **consumer** [notebooklm.google.com](https://notebooklm.google.com) only.
- **Not** Google Cloud NotebookLM Enterprise / Composio enterprise NotebookLM -- different product.
- There is **no official public consumer API**. Community MCPs use **unofficial session / cookie auth** (reverse-engineered). Never claim official Google API support.
- **Never print cookies, tokens, or session files.** Prefer a dedicated Google account for automation.

## Primary recommendation

Use **[@roomi-fields/notebooklm-mcp](https://github.com/roomi-fields/notebooklm-mcp)**:

```bash
# One-time auth in a real terminal (visible Chrome). Do not run interactive login through the agent.
npx -y -p @roomi-fields/notebooklm-mcp notebooklm-mcp-setup-auth
```

Cursor `~/.cursor/mcp.json` snippet (merge into existing `mcpServers`):

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

Requires Node.js >= 18. After saving, reload Cursor / restart MCP servers.

## Verify

1. Confirm the `notebooklm` (or configured) server is connected in Cursor MCP settings.
2. List tools from that server. Use **only** the names the server exposes (typical illustrations only: `notebook_list`, `source_add`, `notebook_ask` -- labels may differ by version).
3. If tools are empty or the server errors, re-run setup-auth in a terminal, check Node version, and review the package README -- do not invent fix commands.

## If MCP install fails

Fall back to the **browser** workflow on https://notebooklm.google.com (see `notebooklm-sources` and `notebooklm-query` skills). Do not invent a fake API client or tool slugs.

## Alternatives (only if user prefers)

Mention briefly: PleasePrompto/notebooklm-mcp, jacob-bd/gemini-notebook-mcp-cli (`nlm` / `notebooklm-mcp-cli`). Install **one** server only to avoid duplicate overlapping tools.
