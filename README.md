[![npm version](https://img.shields.io/npm/v/@robot-resources/scraper-mcp)](https://www.npmjs.com/package/@robot-resources/scraper-mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/robot-resources/scraper-mcp/blob/main/LICENSE)

# @robot-resources/scraper-mcp

> MCP server for Scraper — context compression for AI agents.

[![Robot Resources Scraper MCP server](https://glama.ai/mcp/servers/robot-resources/scraper-mcp/badges/card.svg)](https://glama.ai/mcp/servers/robot-resources/scraper-mcp)

## What is Robot Resources?

**Human Resources, but for your AI agents.**

Robot Resources gives AI agents two superpowers:

- **Router** — Routes each LLM call to the cheapest capable model. 60-90% cost savings across OpenAI, Anthropic, and Google.
- **Scraper** — Compresses web pages to clean markdown. 70-80% fewer tokens per page.

Both run locally. Your API keys never leave your machine. Free, unlimited, no tiers.

### Install the full suite

```bash
npx robot-resources
```

One command sets up everything. Learn more at [robotresources.ai](https://robotresources.ai)

---

## About this MCP server

This package gives AI agents two tools to compress web content into token-efficient markdown via the [Model Context Protocol](https://modelcontextprotocol.io): single-page compression and multi-page BFS crawling.

## Installation

```bash
npx @robot-resources/scraper-mcp
```

Or install globally:

```bash
npm install -g @robot-resources/scraper-mcp
```

## Claude Desktop Configuration

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "scraper": {
      "command": "npx",
      "args": ["-y", "@robot-resources/scraper-mcp"]
    }
  }
}
```

## Tools

### `scraper_compress_url`

Compress a single web page into markdown with 70-90% fewer tokens.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `url` | string | yes | — | URL to compress |
| `mode` | string | no | `'auto'` | `'fast'`, `'stealth'`, `'render'`, or `'auto'` |
| `timeout` | number | no | `10000` | Fetch timeout in milliseconds |
| `maxRetries` | number | no | `3` | Max retry attempts (0-10) |

**Example prompt:** "Compress https://docs.example.com/getting-started"

### `scraper_crawl_url`

Crawl multiple pages from a starting URL using BFS link discovery.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `url` | string | yes | — | Starting URL to crawl |
| `maxPages` | number | no | `10` | Max pages to crawl (1-100) |
| `maxDepth` | number | no | `2` | Max link depth (0-5) |
| `mode` | string | no | `'auto'` | `'fast'`, `'stealth'`, `'render'`, or `'auto'` |
| `include` | string[] | no | — | URL patterns to include (glob) |
| `exclude` | string[] | no | — | URL patterns to exclude (glob) |
| `timeout` | number | no | `10000` | Per-page timeout in milliseconds |

**Example prompt:** "Crawl the docs at https://docs.example.com with max 20 pages"

## Fetch Modes

| Mode | How | Use when |
|------|-----|----------|
| `'fast'` | Plain HTTP | Default sites, APIs, docs |
| `'stealth'` | TLS fingerprint impersonation | Anti-bot protected sites |
| `'render'` | Headless browser (Playwright) | JS-rendered SPAs |
| `'auto'` | Fast → stealth fallback on 403/challenge | Unknown sites (default) |

Stealth requires `impit` and render requires `playwright` as peer dependencies of `@robot-resources/scraper`.

## Requirements

- Node.js 18+

## Related

- [@robot-resources/scraper](https://npm.im/@robot-resources/scraper) - Core compression library
- [@robot-resources/router-mcp](https://npm.im/@robot-resources/router-mcp) - MCP server for LLM cost optimization
- [Robot Resources](https://robotresources.ai) - Human Resources, but for your AI agents

## License

MIT