# Install for Claude Code

Use the same core instructions in [`SKILL.md`](./SKILL.md). Do not fork a divergent rule set.

1. Add project instructions that include or link to `SKILL.md`.
2. For live Notify tool calls during the session, configure MCP:

```json
{
  "mcpServers": {
    "notify": {
      "command": "npx",
      "args": ["-y", "notifycx-mcp"],
      "env": { "NOTIFY_API_KEY": "nk_..." }
    }
  }
}
```

3. Put production send in the app with `notifycx` or `fetch` — MCP does not replace that.

Docs: https://notify.cx/mcp · Source: https://github.com/notifycx/notifycx
