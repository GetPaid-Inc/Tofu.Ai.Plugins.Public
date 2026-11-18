---
name: client-overview
description: Use when the user asks for everything about one client in Tofu Field Service (contacts, what they owe, open invoices, estimates, jobs and notes).
---

# Client overview

1. Call `search_clients` with `name`. If several clients match, ask which one is meant before returning contacts or balances. Never merge their records.
2. Call `get_client` with the selected `client_id` for contacts, balances per currency, open invoices, estimates, jobs and recent notes. Use only returned data; missing or restricted sections are unavailable, not zero.
3. The card contains at most 10 open invoices, estimates and jobs and 5 notes. If counts show more, label the summary partial. For a request for everything, read the remaining results with `search_invoices` (`client_id`, `status` unpaid), `search_estimates` (`client_id`, `statuses` draft, sent, approved), `search_jobs` (`client_id`, `status` all_open) following their cursors. For a request for everything, always call `search_notes` with `client_id` and `page_size` 100: the client card has no notes count. Follow `next_cursor` as `cursor` for remaining notes. If `has_more` remains true without a usable cursor, explicitly say the notes are incomplete.
4. Answer in the user's language with short sections: contacts, money, open work, notes. Keep currencies separate. Distinguish refunds and disputes when visible; do not claim the balance includes every deposit or refund unless the server data proves it. For invoices or estimates with no send record, do not infer delivery or call them drafts.
5. Give the client's `app_url`. Changes and sending are available only in the Tofu app.
