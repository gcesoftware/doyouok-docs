# Doyouok MCP server

[![mcptry](https://mcptry.com/badge/com.doyouok/doyouok)](https://mcptry.com/servers/com.doyouok/doyouok)

Remote MCP server (Streamable HTTP) at **`https://doyouok.com/mcp`**. It lets AI assistants and agents add a heartbeat
check to the cron jobs and automations they build, so you are alerted when a run is missed or fails.

Listed in the official MCP Registry as [`com.doyouok/doyouok`](https://registry.modelcontextprotocol.io/v0/servers?search=com.doyouok/doyouok).
The registry metadata is in [`server.json`](server.json).

## Authentication

Send `Authorization: Bearer dyo_...`, an API token from [doyouok.com](https://doyouok.com) (Profile > API tokens).
The free plan is enough.

## Tools

| Tool | What it does |
|---|---|
| `register_check(name, intervalMinutes=1440, externalId?, source?)` | Creates the check on the first call (idempotent by source + externalId) and returns its `pingUrl`. |
| `list_checks()` | Lists your checks with status, interval, last ping and ping URL. |
| `get_setup_guide()` | Returns setup snippets for n8n, Make, Zapier, Power Automate, cron, Python and email. No token needed. |

After `register_check`, call the returned `pingUrl` at the end of each successful run
(`/fail` with a reason for a failed one). Doyouok alerts by email, Telegram, Slack or Discord when a run fails or
no ping arrives within the interval.

## Client configuration

```json
{
  "mcpServers": {
    "doyouok": {
      "type": "http",
      "url": "https://doyouok.com/mcp",
      "headers": { "Authorization": "Bearer dyo_..." }
    }
  }
}
```

Claude Code:

```sh
claude mcp add --transport http doyouok https://doyouok.com/mcp --header "Authorization: Bearer dyo_..."
```

More: [API reference](https://doyouok.com/docs/api) · [OpenAPI spec](https://doyouok.com/openapi.json) · [llms.txt](https://doyouok.com/llms.txt)
