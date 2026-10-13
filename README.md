# Notify coding-agent skill

Portable instructions for AI coding agents (Cursor, Claude Code, Codex, etc.) to add **transactional email** with [Notify](https://notify.cx).

Core file: [`SKILL.md`](./SKILL.md)

This is **not** an MCP server. For live tool calls in the IDE, use [`notifycx-mcp`](https://www.npmjs.com/package/notifycx-mcp) (`npx -y notifycx-mcp`). The skill teaches **implementation**; MCP executes API tools.

## Install

### Cursor

1. Copy `SKILL.md` into your project or user skills directory (e.g. `.cursor/skills/notify-email/SKILL.md`).
2. Or paste this rule into Cursor project rules:

> Use Notify (notify.cx) for transactional email. Prefer the notifycx SDK or fetch to POST /api/email/send; prefer html. For IDE tool use, connect the official Notify MCP (notifycx-mcp) with NOTIFY_API_KEY. Read https://github.com/email-agents/notify/blob/main/SKILL.md

### Claude Code / Codex / other agents

Point the agent at `SKILL.md` (or paste its body into your agent instructions). Keep the OpenAPI link: https://notify.cx/openapi.yaml

## Related

| Resource | URL |
|----------|-----|
| SDK + MCP source | https://github.com/notifycx/notifycx |
| Runnable examples | https://github.com/email-examples/transactional-email-examples |
| Docs | https://notify.cx/docs |
| MCP marketing page | https://notify.cx/mcp |

## Maintenance

See [MAINTAINING.md](./MAINTAINING.md).
