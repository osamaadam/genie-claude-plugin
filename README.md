# Genie Expense Tracker plugin

Connect Claude, and compatible ChatGPT/Codex marketplace clients where they support Agent Plugins 1.0, to Genie's private read-only remote MCP server. The package includes the shared Agent Plugins manifest, Claude marketplace metadata, the Genie finance skill, and a Streamable HTTP MCP configuration.

## What Genie can provide

After you authorize the connection, Genie can provide read-only:

- Account and card balances with `list_accounts`.
- Transaction search, detail, and aggregation.
- A net-worth snapshot with `get_net_worth`, including primary currency, valued accounts, excluded accounts, unvalued items, completeness, and valuation dates.
- Investment positions and provider/account context with `list_investment_holdings` when investments are enabled and discoverable.
- Subscription and installment summaries.
- Stored financial SMS search and detail only with the separately authorized `sms:read` permission.

The connector cannot create, change, delete, or pay anything. Net worth and holdings are snapshots, not returns or performance tracking. When a response is partial, follow its `is_complete`, inclusion/exclusion, valuation, and FX-date fields; never add `list_accounts` balances to reconstruct net worth.

## Install from this repository

In Claude or Claude Desktop, open **Customize → Plugins**, select **+ → Add marketplace**, and enter:

```text
https://github.com/osamaadam/genie-claude-plugin
```

Install **Genie Expense Tracker**, enable it, and complete the Genie authorization flow when prompted. The same repository contains an Agent Plugins 1.0 package for compatible ChatGPT/Codex marketplace clients where that package format is supported; client and workspace availability can differ.

## Install for development

Clone this repository, then run Claude Code from its parent directory:

```sh
claude --plugin-dir ./genie-claude-plugin
```

Open `/mcp` in Claude Code and complete OAuth for the `genie` server. You can also validate the Claude package with:

```sh
claude plugin validate ./genie-claude-plugin --strict
```

## Connect without the plugin

The same server is available directly over Streamable HTTP:

```sh
claude mcp add --transport http genie https://genie-mobile.duckdns.org/mcp
```

In Claude on the web or Claude Desktop, open **Customize → Connectors → Add custom connector** and enter:

```text
https://genie-mobile.duckdns.org/mcp
```

## Authentication and privacy

Genie uses OAuth. Enter your Genie account number only on the authorization page hosted at `https://genie-mobile.duckdns.org`; never paste it into Claude, a plugin configuration, an issue, or a support message.

The optional `sms:read` permission allows the connector to return complete stored financial SMS messages. Grant it only if you want Claude to inspect those messages.

- [Connection guide](https://genie-mobile.duckdns.org/agents)
- [Privacy policy](https://genie-mobile.duckdns.org/privacy)
- [Terms of service](https://genie-mobile.duckdns.org/terms)
- [Support](https://genie-mobile.duckdns.org/support)
- [Delete Genie data](https://genie-mobile.duckdns.org/delete-data)

## Security reports

Report vulnerabilities privately to [osamaadamme@gmail.com](mailto:osamaadamme@gmail.com). Do not open a public issue containing account numbers, tokens, authorization codes, financial records, or SMS messages.

## License

The plugin metadata and skill instructions in this repository are available under the [MIT License](LICENSE). The license does not apply to the separate Genie application or backend service.
