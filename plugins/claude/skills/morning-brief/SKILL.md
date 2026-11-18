---
name: morning-brief
description: Use when the user asks what needs their attention today or wants a morning brief for their Tofu Field Service business.
---

# Morning brief

Read the selected business with `get_business` and `get_balances`. If `getting_started.is_empty` is true, show its `guide_markdown` in full, preserving every step and URL in the user's language, then stop. Otherwise gather evidence for these blocks and present them in this order:

1. Debt and overdue invoices: `search_invoices` with `status` unpaid. Keep currencies separate. Show refunds and disputes returned by `get_balances` separately; do not treat an unverified aggregate as reconciled net debt.
2. Invoices with no send record in Tofu, as part of unpaid invoices when supported. Sharing by text, link or PDF is not observed; no send record does not prove the document is a draft or was not received.
3. Disputed payments, separately from debt, only if returned status identifies them.
4. Today's visits: `search_visits`, converted to the business timezone before selecting the day, grouped by job and time with all returned workers; mark unassigned visits. If timezone is unknown, label UTC.
5. Estimates waiting over seven days: `search_estimates` with `statuses` ["sent"], then `get_estimate` or `search_activity` for evidence of sending. State days waiting only if a send timestamp is actually available. A recent event page does not prove the first send date. Mention estimates with no send record separately; do not add them to the verified waiting total.
6. Approved estimates not on the schedule: `search_estimates` with `statuses` ["approved"] and `get_estimate`, then linked `get_job`. A missing link does not prove no job exists. Search that client's jobs before making that claim; call an unlinked candidate a possible match. A linked job with no visits is not scheduled.
7. Work done without an invoice: inspect `search_jobs` and `get_job`. Distinguish explicitly completed jobs, all visits completed, and past visits without completion marks. The last case needs the owner's check. A completed-only filter is not enough to find all three cases. Do not infer completion from dates alone.
8. Client activity since yesterday: `search_activity` with `since` converted from the business timezone. Identify the action only when the event supports it. Say "the email was opened", not that the client read or received the document. Opening may be automatic; do not infer a human or client actor from an ambiguous event or an estimate status.

Follow `next_cursor`, narrow filters for `has_more`, and label any remaining incomplete coverage. Omit blocks verified empty; explicitly flag blocks that cannot be verified because data is missing or access is restricted. Never turn unavailable data into a zero or an empty result. Do not invent amounts, statuses, timestamps or relationships. Answer in the user's language. This workflow only reads; link to the Tofu app for actions.
