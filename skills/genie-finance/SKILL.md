---
name: genie-finance
description: Analyze the user's Genie Expense Tracker accounts, transactions, net worth, investments, subscriptions, installments, and financial summaries. Use when the user asks about Genie finances, spending, income, balances, holdings, recurring charges, or installment plans.
---

# Genie finance analysis

Use the Genie connector for the user's private financial data. Genie is read-only: do not imply that it can create, edit, delete, or pay anything.

## Choose the narrowest tool

- Use `list_accounts` for accounts, cards, currencies, and current balances. Do not add its balances together to reconstruct net worth.
- Use `get_net_worth` for a current net-worth snapshot. Report its primary currency, `total_minor` (integer minor units in that output currency; `null` means unavailable), `valued_at`, included accounts, excluded accounts, and `unvalued_items` as returned.
- Use `list_investment_holdings` for investment positions, provider breakdown, account context, and holding valuation dates. It is available only when Genie investments are enabled and discoverable.
- Use `aggregate_transactions` for totals, trends, and grouping by category, merchant, account, or period.
- Use `search_transactions` for filtered transaction lists. Use bounded date ranges and page only when the user needs more results.
- Use `get_transaction` when one transaction needs complete detail.
- Use `list_subscriptions` for recurring charges and expected renewal dates.
- Use `list_installments` for installment plans and payoff forecasts.
- Use `search_sms` or `get_sms` only when the user explicitly asks to inspect stored financial messages. These tools require the separately authorized `sms:read` scope and can return complete message bodies.

## Present results carefully

- Net worth and holdings are point-in-time snapshots, not return, profit, loss, or performance tracking. Never infer performance from one snapshot or from a holding value.
- `get_net_worth` is complete only when `is_complete` is true. If it is false, explain that included accounts may still contribute their known primary-currency value, while excluded or unvalued accounts remain separately listed and are not silently treated as zero. An incomplete excluded account does not change top-level completeness, which describes included accounts only. Always disclose `valued_at` and any account or item valuation/FX dates supplied by the response.
- For `list_investment_holdings`, identify the provider and account for each position, preserve the flat holding list, report each holding's `is_complete` (disclosing when it is false), and explain that it covers native quote valuation only. Use `get_net_worth` account rows for account-level FX dates and conversion completeness.
- Preserve currency labels and distinguish original-currency values from converted primary-currency values.
- State the time range and filters behind every transaction summary.
- Distinguish expenses, income, transfers, and balance adjustments.
- Treat merchant/category matches and subscription detection as recorded classifications, not certainty about the user's intent.
- If results are incomplete or paginated, say so instead of presenting them as exhaustive.
- Never ask the user to paste their Genie account number, OAuth codes, access tokens, refresh tokens, or SMS bodies into chat. Authentication happens only on `https://genie-mobile.duckdns.org`.
