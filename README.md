# The White Report — MCP Server

**Remote MCP server for The White Report** (thewhitereport.com — "Where AI meets money": crypto and AI news, written for humans and structured for machines).

- **Endpoint:** `https://thewhitereport.com/mcp.php`
- **Transport:** Streamable HTTP (stateless JSON-RPC over POST)
- **Auth:** None — public, read-only, free
- **Server name / version:** `white-report` v0.1.0
- **Info for agents & builders:** https://thewhitereport.com/agents

This repository contains the public listing metadata (`server.json`, `glama.json`) and documentation for the hosted server. The server itself runs at the endpoint above; no local install is required or offered.

## Tools

| Tool | Description |
| --- | --- |
| `get_latest` | Newest White Report articles (headline, summary, dates, URLs). Optional `limit` (1–20, default 5). |
| `search_articles` | Search the article archive by keyword (headline, summary, key facts, entities, tickers). Requires `query`; optional `limit` (1–20, default 10). |
| `get_article` | Full machine-readable article (the JSON twin: facts, sources, call, full text). Requires `slug`. |
| `get_ticker` | Market snapshot: crypto top 5, AI stocks, and metrics, with the snapshot timestamp. |
| `get_scoreboard` | Every dated public call The White Report has made, its grade date, and its grade (`null` while pending). |
| `calls_list` | Machine format (`wr.calls.v1`): sealed per-call envelopes from the graded-calls ledger, with optional `state` / `asset` filters. |
| `calls_get` | Machine format (`wr.calls.v1`): the full sealed envelope for one `call_id`. |
| `calls_since` | Machine format (`wr.calls.v1`): call envelopes with `published_at` after an ISO-8601 UTC timestamp. |
| `event_briefs_list` | Machine format (`wr.event.v1`): the scheduled-event coverage calendar and brief index. |
| `event_brief_get` | Machine format (`wr.event.v1`): one sealed event brief envelope by `id` (optional `version`, default latest). |
| `telemetry_latest` | Machine format (`wr.telemetry.v1`): the latest sealed compile envelope per telemetry metric (optional `metric` filter). |
| `telemetry_series` | Machine format (`wr.telemetry.v1`): every sealed compile envelope for one `metric`, oldest first. |

Naming note (2026-11-12, TDQS cure): the tool names mix conventions by family — article tools are verb-first (`get_*`, `search_articles`), machine-format families are family-first (`calls_*`, `event_briefs_*`/`event_brief_get`, `telemetry_*`, mirroring their `wr.*.v1` format ids). The names are a live public contract (referenced by the site's agent setup instructions and external clients), so they were **not** renamed; instead each tool's description now names its family, its siblings, and its distinct job. A rename, if ever done, needs a versioned endpoint with an old→new mapping and a deprecation window.

## Connect

### Claude Code

```bash
claude mcp add --transport http white-report https://thewhitereport.com/mcp.php
```

### MCP client config (Claude Desktop via `mcp-remote`, Cursor, VS Code, Windsurf, etc.)

```json
{
  "mcpServers": {
    "white-report": {
      "url": "https://thewhitereport.com/mcp.php"
    }
  }
}
```

For clients that only support stdio servers, bridge with `mcp-remote`:

```json
{
  "mcpServers": {
    "white-report": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://thewhitereport.com/mcp.php"]
    }
  }
}
```

## Citation & reuse

Facts and figures may be quoted with attribution — "The White Report (thewhitereport.com)" — and a link to the source article. Republishing complete articles requires permission; summaries and facts with attribution do not. When an article makes a call, the JSON twin carries it verbatim, and The White Report grades its calls publicly after the fact (see `get_scoreboard`).

## Also available

- Per-article JSON twins: `https://thewhitereport.com/f/{slug}.json`
- Site descriptor: https://thewhitereport.com/agents.json
- Plain-text site map: https://thewhitereport.com/llms.txt
- RSS: https://thewhitereport.com/feed.xml

Published by Cyan Eclipse Technologies LLC.
