# Tofu for Claude Code

This plugin is for Tofu Field Service accounts. It lets Claude read one selected business: invoices, estimates, clients, jobs, schedule, team and the business's own price list. It cannot create or change records, send invoices or reminders, or take payments. Use the Tofu app for those actions.

## Install and connect

1. Install the plugin in Claude Code:

   ```bash
   claude plugin marketplace add GetPaid-Inc/Tofu.Ai.Plugins.Public
   claude plugin install tofu@tofu-plugins
   ```

2. Run `/mcp` and choose `plugin:tofu:tofu` to connect.
3. Sign in with your Tofu account, choose the business and press Allow.

Ask in your own language, for example:

- Who owes me money? What is overdue?
- What is on my schedule today?
- What needs my attention today?

## Skills

| Skill | What it reads |
|---|---|
| `who-owes-me` | Outstanding and overdue invoices, grouped by client and currency |
| `whats-on-today` | Visits and jobs on the schedule, including unassigned visits |
| `client-overview` | One client's contacts, balances, open invoices, estimates, jobs and notes |
| `suggest-price` | Matching entries in the business's own price list, with unset prices identified |
| `morning-brief` | An ordered business summary with missing evidence and incomplete coverage identified |

## Data sent to Claude

The package contains instructions and a connection to the Tofu MCP server at `https://api.tofu.com/mcp`. After you authorize access, Claude sends tool requests to Tofu. Tofu returns records from the business you selected, subject to your role and plan permissions, and Claude uses those responses to answer your questions.

Responses can include business and client contact details, invoice and estimate contents and balances, jobs and visits, team members, notes and price-list entries. Missing or restricted data is identified in the answer. Installing the plugin does not authorize access by itself; you must connect your Tofu account separately.

Tofu's [privacy policy](https://tofu.com/legal/privacy), [terms](https://tofu.com/legal/terms) and [support contacts](https://tofu.com/legal/contacts) are on the Tofu website.

## Disconnect

Disconnect or remove the Tofu connector in Claude's connector settings. In Claude Code, run `/mcp`, choose `plugin:tofu:tofu` and clear the authentication.
