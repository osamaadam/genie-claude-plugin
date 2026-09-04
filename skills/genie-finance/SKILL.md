---
name: genie-finance
description: Analyze the user's Genie Expense Tracker accounts, transactions, subscriptions, installments, and financial summaries. Use when the user asks about their Genie finances, spending, income, balances, recurring charges, or installment plans.
---

# Genie finance analysis

Use the Genie connector for the user's private financial data. Genie is read-only: do not imply that it can create, edit, delete, or pay anything.

## Choose the narrowest tool

- Use `list_accounts` for accounts, cards, currencies, and current balances.
- Use `aggregate_transactions` for totals, trends, and grouping by category, merchant, account, or period.
- Use `search_transactions` for filtered transaction lists. Use bounded date ranges and page only when the user needs more results.
- Use `get_transaction` when one transaction needs complete detail.
- Use `list_subscriptions` for recurring charges and expected renewal dates.
- Use `list_installments` for installment plans and payoff forecasts.
- Use `search_sms` or `get_sms` only when the user explicitly asks to inspect stored financial messages. These tools require the separately authorized `sms:read` scope and can return complete message bodies.

## Present results carefully

- Preserve currency labels and distinguish original-currency values from converted primary-currency values.
- State the time range and filters behind every summary.
- Distinguish expenses, income, transfers, and balance adjustments.
- Treat merchant/category matches and subscription detection as recorded classifications, not certainty about the user's intent.
- If results are incomplete or paginated, say so instead of presenting them as exhaustive.
- Never ask the user to paste their Genie account number, OAuth codes, access tokens, refresh tokens, or SMS bodies into chat. Authentication happens only on `https://genie-mobile.duckdns.org`.
