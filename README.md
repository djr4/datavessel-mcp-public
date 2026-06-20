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

1. **Create your account** — sign up at [www.datavessel.io](https://www.datavessel.io)
   and connect the data sources you want (Google, Shopify, etc.) via OAuth in the
   [dashboard](https://app.datavessel.io). See [datavessel.io/mcp](https://datavessel.io/mcp)
   for the full MCP overview.
2. **Add the server to your MCP client** using the remote Streamable HTTP URL
   `https://mcp.datavessel.io/mcp`.

**Authentication is handled automatically over OAuth — there is no API key to
copy or paste.** datavessel implements the MCP authorization spec: the first time
you connect, your client discovers the server's OAuth metadata, **registers itself
dynamically (DCR)**, and opens a browser to sign you in. Tokens (with PKCE) are
issued and refreshed by the client for you.

### Clients with native remote MCP support (Claude, etc.)

Add the remote server by URL — your client runs the OAuth flow on first connect:

```json
{
  "mcpServers": {
    "datavessel": {
      "type": "streamable-http",
      "url": "https://mcp.datavessel.io/mcp"
    }
  }
}
```

### Clients without native remote support (via `mcp-remote`)

`mcp-remote` bridges a stdio client to the remote server and performs the same
OAuth/DCR handshake — again, **no token in the config**:

```json
{
  "mcpServers": {
    "datavessel": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.datavessel.io/mcp"]
    }
  }
}
```

On first connect a browser window opens to authorize datavessel; approve it once
and the tools appear. If a connection ever fails with an auth error, clear your
client's saved tokens and reconnect — it will re-register automatically.

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
