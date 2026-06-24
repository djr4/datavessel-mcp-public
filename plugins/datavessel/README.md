# datavessel plugin for Claude Code

Connect your agent to **100+ read/write tools** across Google Analytics 4,
Search Console, Google & Meta Ads, Shopify, WooCommerce, Shopware, Slack and
LinkedIn — through the hosted, remote **datavessel MCP server**. Bring your own
key (BYOK); auth is handled over OAuth, nothing to install or run.

The plugin bundles:

- **MCP server** (`.mcp.json`) — the remote datavessel server at
  `https://mcp.datavessel.io/mcp`. On first use your client discovers the OAuth
  metadata, registers itself (DCR), and opens a browser to sign you in.
- **`datavessel` skill** (`skills/datavessel`) — guidance for driving the
  [datavessel CLI](https://github.com/djr4/datavessel-cli) (`dv`) from the
  terminal, including discovering tools at runtime and gathering data across
  parallel subagents.

## Install

```text
/plugin marketplace add djr4/datavessel-mcp-public
/plugin install datavessel@datavessel
```

Then connect your data sources (Google, Shopify, …) in the
[dashboard](https://app.datavessel.io). See
[datavessel.io/mcp](https://datavessel.io/mcp) for the full overview.
