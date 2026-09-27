# Mooncatcher Wire MCP server

Free crypto news for AI agents. Mooncatcher Wire runs a remote [Model Context Protocol](https://modelcontextprotocol.io) server over the same board as [mooncatcherwire.com](https://www.mooncatcherwire.com/): every crypto wire story of the last cycle, deduplicated and scored by AI for sentiment and market impact, plus an AI market digest, search and topics.

**No API key. No account. Nothing to install.**

```
https://mooncatcherwire.com/mcp
```

Streamable HTTP, JSON-RPC 2.0, protocol versions `2025-06-18` and `2025-03-26`. Send no `Authorization` header.

Official MCP Registry: [`com.mooncatcherwire/wire`](https://registry.modelcontextprotocol.io/v0/servers?search=com.mooncatcherwire)

## Add it to your client

**Claude (claude.ai and Claude Desktop):** Settings → Connectors → Add custom connector → `https://mooncatcherwire.com/mcp`

**Claude Code**

```sh
claude mcp add --transport http mooncatcherwire https://mooncatcherwire.com/mcp
```

**Cursor, Windsurf and other clients with an `mcpServers` file**

```json
{
  "mcpServers": {
    "mooncatcherwire": { "url": "https://mooncatcherwire.com/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "mooncatcherwire": { "type": "http", "url": "https://mooncatcherwire.com/mcp" }
  }
}
```

**By hand**

```sh
curl -s https://mooncatcherwire.com/mcp \
  -H 'content-type: application/json' -H 'accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"mcw-get-board","arguments":{"limit":5}}}'
```

## Tools

All six tools are read-only.

| Tool | What it does |
| --- | --- |
| `mcw-get-board` | The current board: mood, counts, top stories by market impact, and the AI digest. Start here. |
| `mcw-list-stories` | Stories filtered by ticker (BTC, ETH, SOL…), topic, age, or breaking only. |
| `mcw-get-story` | One story in full, by id. |
| `mcw-search` | Case-insensitive search over headlines and summaries. |
| `mcw-list-topics` | The topics and the keyword rules behind them. |
| `mcw-get-digest` | The AI market digest: overview, bull/neutral/bear split, per-ticker takeaways. |

The board refreshes every five minutes.

## Limits

- 30 requests a minute and 1,000 a day, per IP, without an account.
- Over a limit you get a JSON-RPC error naming the limit and a `Retry-After` header.
- Optional OAuth 2.1 (scope `news:read`) for account holders. See [auth.md](https://mooncatcherwire.com/auth.md).

## Links

- Website: https://www.mooncatcherwire.com/
- Setup page for agents: https://www.mooncatcherwire.com/agents/
- RSS: https://www.mooncatcherwire.com/feed.xml · JSON Feed: https://www.mooncatcherwire.com/feed.json
- REST API (OpenAPI): https://www.mooncatcherwire.com/api/v1/openapi.json
- Contact: admin@mooncatcherwire.com

Mooncatcher Wire aggregates news and market sentiment. It is not investment advice.

This repository holds the public listing for the hosted server (this README and `server.json`). The server itself runs at mooncatcherwire.com.
