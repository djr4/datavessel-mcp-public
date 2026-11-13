<div align="center">

# datavessel: the e-commerce MCP server

**Connect Claude, ChatGPT, Claude Code, Codex or n8n to your Shopify, Shopware or
WooCommerce store, and to Merchant Center, Google Ads, Analytics, Search Console,
Meta Ads and Amazon Seller Central.**

[Website](https://datavessel.io) · [App](https://app.datavessel.io) · [MCP](https://datavessel.io/mcp) · [Integrations](https://datavessel.io/integrations) · [Blog](https://blog.datavessel.io) · [Pricing](https://datavessel.io/pricing)

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple.svg)](https://modelcontextprotocol.io)

</div>

> This repository is the public home and setup guide for the **datavessel MCP
> server**. datavessel is a **hosted, remote** MCP server: there is nothing to
> install or run. Add the URL below to your AI client and sign in.

## What it is

One connector that puts your store and the accounts around it in the same
conversation. Your assistant gets 300+ typed, validated tools, so it can answer
questions that need more than one source and then make the change that follows.

- **Hosted and remote.** Streamable HTTP at `https://mcp.datavessel.io/mcp`. No
  local install.
- **Sign in, no keys.** OAuth 2.1 with dynamic client registration and PKCE.
- **Writes are marked.** Every tool carries MCP annotations (`readOnlyHint`,
  `destructiveHint`), so your client can ask before a write runs. Executed
  changes are kept in a change record with the client they came from.
- **Scoped to your store.** You only see tools for the sources you connected.
- **Your model.** The reasoning runs in your own client. datavessel adds no AI
  bill.

Questions it is built for:

- *"Which products are disapproved in Merchant Center and still in an active
  Google Ads campaign?"*
- *"Which pages lost the most clicks in Search Console in the last 28 days, and
  what does Analytics say about them?"*
- *"Which of my top twenty SKUs on amazon.de have under two weeks of FBA supply,
  and how many units sit in the shop warehouse?"*
- *"Draft a new meta title for my best-selling product and show me the change
  before you save it."*

## Connectors

| Connector | What your assistant can do |
|---|---|
| **Shopify** | Orders, products, customers, inventory, fulfilment and tracking, discounts |
| **WooCommerce** | Orders, products, customers, sales reports, coupons, inventory |
| **Shopware** | Storefront and admin reads, orders and state changes, products, CMS and landing pages, SEO URLs |
| **Google Merchant Center** | Feed health, disapproved products, price insights, best sellers; product updates and promotions |
| **Google Ads** | Campaign, ad group, keyword, product and search-term performance; status, budgets, bidding, keywords and new campaigns |
| **Google Analytics 4** | Traffic, realtime, checkout funnel, custom reports |
| **Google Search Console** | Search performance, top queries and pages, URL inspection, sitemaps, keyword opportunities |
| **Google Tag Manager** | Read-only: containers, versions, workspace status, event tracing, consent audit |
| **Meta Ads** | Campaigns, ad sets, ads and insights; pause or resume, and budgets |
| **Amazon Seller Central** | Orders, sales, FBA stock, fees, listing issues and catalog search across nine European marketplaces; listing updates. No buyer data |
| **Klaviyo** | Campaigns, flows, lists, segments, metrics and profiles; campaign drafts and list changes |
| **Judge.me** | Reviews and reviewers; replies, curation and review requests |
| **Gorgias** | Tickets, messages, macros and satisfaction surveys; replies, notes, tags and status |
| **HubSpot** | Read-only: contacts, companies, deals, tickets and pipelines |
| **Slack** | Channels, threads and messages; post messages and DMs |
| **WordPress** | Posts, categories and tags; create and update posts, upload media |
| **Also** | Google Business Profile (reviews and replies) and LinkedIn (posts) |

The current list of connectors is at
[datavessel.io/integrations](https://datavessel.io/integrations).

The platforms have reviewed the app: Google has verified it, Meta has approved
its ads access, Amazon has approved it for the Selling Partner API, and the
Shopify app is listed in the Shopify App Store.

## Setup

1. **Create your account.** Sign in at [app.datavessel.io](https://app.datavessel.io)
   with Google.
2. **Connect your store**: Shopify, WooCommerce or Shopware. The store's card
   then connects its Google accounts, Meta Ads, Amazon and the other tools.
3. **Add the server to your client** with the URL `https://mcp.datavessel.io/mcp`.

**Claude (desktop, web, mobile).** Settings, then Connectors, then *Add custom
connector*. Name it `datavessel`, paste the URL, and sign in with the same
account.

**ChatGPT.** Turn on Developer mode under Settings, Connectors, Advanced. Then
create a connector with the URL and sign in.

**Claude Code.**

```bash
claude mcp add --transport http datavessel https://mcp.datavessel.io/mcp
```

Then run `/mcp` to sign in.

**Other clients with remote MCP support.** Add the server by URL; the client
runs the sign-in on first connect:

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

**Clients without remote support.** `mcp-remote` bridges a stdio client to the
remote server and performs the same sign-in, with no token in the config:

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

### Authentication

There is no API key to copy or paste. datavessel implements the MCP
authorization spec: the first time you connect, your client discovers the
server's OAuth metadata, registers itself dynamically (DCR), and opens a browser
to sign you in. Tokens (with PKCE) are issued and refreshed by the client for
you. If a connection ever fails with an auth error, clear your client's saved
tokens and reconnect.

## Pricing

Reads are free and unlimited. Plans count writes, and 50 writes a month are
free. Stores are not counted. Current plans:
[datavessel.io/pricing](https://datavessel.io/pricing).

## Guides

- [Connect Claude to your store](https://blog.datavessel.io/connect-claude-to-your-store/)
- Connect ChatGPT to [Shopify](https://blog.datavessel.io/connect-chatgpt-to-shopify/),
  [Shopware](https://blog.datavessel.io/connect-chatgpt-to-shopware/) or
  [WooCommerce](https://blog.datavessel.io/connect-chatgpt-to-woocommerce/)
- MCP servers compared: [Shopify](https://blog.datavessel.io/shopify-mcp-server/),
  [Shopware](https://blog.datavessel.io/shopware-mcp-server/)
  ([Deutsch](https://blog.datavessel.io/shopware-mcp-server-vergleich/)),
  [WooCommerce](https://blog.datavessel.io/woocommerce-mcp-server/)
- [Amazon Seller Central MCP](https://blog.datavessel.io/amazon-seller-central-mcp/)
- [Google Merchant Center MCP](https://blog.datavessel.io/google-merchant-center-mcp/)
- [Google Tag Manager MCP](https://blog.datavessel.io/google-tag-manager-mcp/)

The same tools run from the terminal with the
[datavessel CLI](https://github.com/djr4/datavessel-cli).

## Links and support

- Website: https://datavessel.io
- App: https://app.datavessel.io
- MCP details: https://datavessel.io/mcp
- Blog: https://blog.datavessel.io
- Support: [open an issue](../../issues) or write to contact@datavessel.io

## License

Apache-2.0. See [LICENSE](./LICENSE).
