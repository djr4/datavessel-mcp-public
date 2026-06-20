<div align="center">

# datavessel — MCP server for your marketing & ecommerce stack

**Connect your AI agent to 100+ read/write tools across Google Analytics, Search
Console, Google & Meta Ads, Shopify, WooCommerce, Shopware, Slack and LinkedIn.**

[Website](https://www.datavessel.io) · [App](https://app.datavessel.io) · [MCP](https://datavessel.io/mcp) · [Blog](https://blog.datavessel.io) · [Pricing](https://www.datavessel.io/pricing)

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple.svg)](https://modelcontextprotocol.io)

</div>

> This repository is the public home and setup guide for the **datavessel MCP
> server**. datavessel is a **hosted, remote** MCP server — there's nothing to
> install or run. Point your AI client at the URL below with your own API key.

## What it is

datavessel gives AI agents (Claude, Cursor, and any MCP client) read **and write**
access to your entire marketing and ecommerce stack through a single connection.
One agent, your whole stack — pull data *and* take action.

- **Bring your own key (BYOK).** Your data, your credentials.
- **Hosted & remote.** No local install; Streamable HTTP.
- **100+ typed tools across 10 connectors**, plus 20+ guided workflows.

## Connectors

| Connector | What your agent can do |
|---|---|
| **Google Analytics 4** | Traffic, realtime, custom reports, property config |
| **Google Search Console** | Search performance, top queries/pages, sitemaps, keyword opportunities |
| **Google Ads** | Campaign, ad-group, keyword & search-term performance |
| **Meta Ads** | Campaigns, ad sets, ads, account & campaign insights |
| **Shopify** | Orders, products, customers, inventory, discounts — *incl. writes* |
| **WooCommerce** | Orders, products, customers, sales reports, coupons |
| **Shopware** | Catalog, orders, customers — *create/update CMS & landing pages, SEO URLs, products* |
| **Slack** | Channels, history, post messages & DMs |
| **LinkedIn** | Publish text & article posts |
| **datavessel** | Reports, alerts, domain checks & utilities |

> Example: *"Find Search Console keywords where we rank well but get few clicks,
> rewrite those product titles in Shopify, and post the summary to #seo in Slack."*

## Setup

1. **Get an API key** — sign up at [www.datavessel.io](https://www.datavessel.io)
   and create an API key in the [dashboard](https://app.datavessel.io). Connect
   the data sources you want (Google, Shopify, etc.) via OAuth there. See
   [datavessel.io/mcp](https://datavessel.io/mcp) for the full MCP overview.
2. **Add the server to your MCP client.** The connection is remote Streamable
   HTTP at `https://mcp.datavessel.io/mcp`, authenticated with your API key.

### Claude Desktop / Cursor (universal, via `mcp-remote`)

```json
{
  "mcpServers": {
    "datavessel": {
      "command": "npx",
      "args": [
        "-y", "mcp-remote",
        "https://mcp.datavessel.io/mcp",
        "--header", "Authorization: Bearer ${DATAVESSEL_API_KEY}"
      ],
      "env": { "DATAVESSEL_API_KEY": "your-api-key" }
    }
  }
}
```

### Clients with native remote MCP support

```json
{
  "mcpServers": {
    "datavessel": {
      "type": "streamable-http",
      "url": "https://mcp.datavessel.io/mcp",
      "headers": { "Authorization": "Bearer your-api-key" }
    }
  }
}
```

Restart your client; the datavessel tools will appear. Your agent calls
`authenticate` first, then any tool above.

## Pricing

| Tier | API calls | Price |
|---|---|---|
| **Free** | 100 / month | $0 |
| **Professional** | 1,000 / month | $49 / month |

All tools are available on both tiers — discovery calls don't count toward the limit.

## Links & support

- 🌐 Website: https://www.datavessel.io
- 🚀 App / dashboard: https://app.datavessel.io
- 🔌 MCP details: https://datavessel.io/mcp
- ✍️ Blog: https://blog.datavessel.io
- 💬 Support: [open an issue](../../issues) or contact us via the [website](https://www.datavessel.io)

## License

Apache-2.0 — see [LICENSE](./LICENSE).
