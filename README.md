# Genie Expense Tracker for Claude

Connect Claude to your private Genie Expense Tracker data through Genie's read-only remote MCP server. The plugin adds the Genie connector and guidance for analyzing accounts, transactions, spending, income, subscriptions, and installment plans.

## What Claude can access

After you authorize the connection, Claude can use these read-only tools:

- `list_accounts`
- `search_transactions`
- `get_transaction`
- `aggregate_transactions`
- `list_subscriptions`
- `list_installments`
- `search_sms` (requires separate `sms:read` permission)
- `get_sms` (requires separate `sms:read` permission)

The connector cannot create, change, delete, or pay anything.

## Install from Claude's plugin directory

Once the plugin is published, open **Customize → Plugins → Browse plugins**, find **Genie Expense Tracker**, and select **Install**. Enable the plugin and complete the Genie authorization flow when Claude prompts you to connect.

## Install from this repository

In Claude or Claude Desktop, open **Customize → Plugins**, select **+ → Add marketplace**, and enter:

```text
https://github.com/osamaadam/genie-claude-plugin
```

After Claude adds the **Genie Plugins** marketplace, install **Genie Expense Tracker**, enable it, and complete the Genie authorization flow when prompted.

## Install for development

Clone this repository, then run Claude Code from its parent directory:

```sh
claude --plugin-dir ./genie-claude-plugin
```

Open `/mcp` in Claude Code and complete OAuth for the `genie` server. You can also validate the package with:

```sh
claude plugin validate ./genie-claude-plugin --strict
```

## Connect without the plugin

You can add the same remote MCP server directly:

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
