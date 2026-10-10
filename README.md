# SearXNG MCP Server

[![npm](https://img.shields.io/npm/v/@tobioffice/mcp-searxng.svg)](https://www.npmjs.com/package/@tobioffice/mcp-searxng)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![MCP](https://img.shields.io/badge/MCP-compatible-6E56CF)](https://modelcontextprotocol.io)

A [Model Context Protocol](https://modelcontextprotocol.io) server that integrates the [SearXNG](https://docs.searxng.org) API, giving any MCP client private web search and URL-to-Markdown reading through your own meta-search instance.

## Features

- **Web search** against any SearXNG instance - no third-party search API keys
- **Pagination** with page selection
- **Filters**: time range (day/month/year), language, and safe search
- **URL reader**: fetch any URL and convert it to Markdown
- **Authentication**: optional HTTP Basic Auth for protected instances

## Tools

### `searxng_web_search`

Performs a web search and returns titles, descriptions and URLs.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `query` | string | yes | The search query |
| `pageno` | number | no | Search page number, starts at 1 (default `1`) |
| `time_range` | string | no | One of `day`, `month`, `year` |
| `language` | string | no | Language code (e.g. `en`, `fr`, `de`) or `all` (default `all`) |
| `safesearch` | string | no | `0` none, `1` moderate, `2` strict (default `0`) |

### `web_url_read`

Fetches a URL and converts the HTML content to Markdown.

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `url` | string | yes | The URL to fetch and process |

## Configuration

| Environment variable | Default | Description |
| --- | --- | --- |
| `SEARXNG_URL` | `http://localhost:8080` | Base URL of your SearXNG instance |
| `AUTH_USERNAME` | - | Username for HTTP Basic Auth (optional) |
| `AUTH_PASSWORD` | - | Password for HTTP Basic Auth (optional) |

Choose a public instance from [searx.space](https://searx.space/) or run your own.

## Installation

### npx

```json
{
  "mcpServers": {
    "searxng": {
      "command": "npx",
      "args": ["-y", "@tobioffice/mcp-searxng"],
      "env": {
        "SEARXNG_URL": "YOUR_SEARXNG_INSTANCE_URL"
      }
    }
  }
}
```

### npm global install

```bash
npm install -g @tobioffice/mcp-searxng
```

```json
{
  "mcpServers": {
    "searxng": {
      "command": "tobioffice-mcp-searxng",
      "env": {
        "SEARXNG_URL": "YOUR_SEARXNG_INSTANCE_URL"
      }
    }
  }
}
```

### From source

```bash
git clone https://github.com/tobioffice/mcp-searxng.git
cd mcp-searxng
pnpm install
pnpm run build
node dist/index.js
```

Ready-to-copy client configs are included in [`claude_desktop_config_example.json`](claude_desktop_config_example.json) and [`claude_desktop_config_with_auth.json`](claude_desktop_config_with_auth.json).

## Development

```bash
pnpm install
pnpm run build   # compile TypeScript to dist/
pnpm run watch   # compile in watch mode
```

## License

MIT - see [LICENSE](LICENSE).
