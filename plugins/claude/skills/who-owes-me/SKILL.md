---
name: who-owes-me
description: Use when the user asks who owes them money, which invoices are unpaid or overdue, or how much is outstanding in their Tofu Field Service business.
---

# Who owes me

1. Call `get_balances` for the server's totals per currency. If `getting_started.is_empty` is true, show `getting_started.guide_markdown` in full, preserving every step and URL in the user's language, then stop. An empty filtered search alone does not mean the business is empty.
2. Call `search_invoices` with `status` unpaid, first with `overdue` true and then false. Follow `next_cursor` for a complete list; label a partial list. Show refunds and disputes returned by `get_balances` separately from ordinary unpaid invoices. Do not present an unverified aggregate as a reconciled debt total.
3. Group by client, largest debts first within each currency. Show the invoice number, returned amount due and due date. A missing due date is not evidence of overdue debt. Use the business timezone from `get_business` for date boundaries; if it is missing, say UTC is being used. Do not invent days overdue or recompute payment balances without dated payment/refund data.
4. Include unpaid invoices with no send record, and show that portion separately when the returned records support it. Say "no send record in Tofu", never infer "draft", "not received" or "not sent": Tofu does not observe sharing by text, link or PDF. If a breakdown cannot be verified, say it is unavailable.
5. State that payments made outside Tofu appear only after the owner records them in Tofu. Link to the relevant invoices or clients using `app_url` or the server's app-link instructions. Never add different currencies.

Tofu can only read here. For reminders or changes, give the invoice link in the app.
