---
name: suggest-price
description: Use when the user asks what they charge for a service or material in their Tofu Field Service price list, or asks whether Tofu has market prices.
---

# Read the business price list

1. Call `search_items` with `name`. Follow `next_cursor` to find all matching entries, including repeated names. Never pick one rate silently when several match.
2. Show each matching entry's name, description, nonzero price with currency, unit and tax flag. A zero price means "no price set", not a free service. Mark an entry as a system template only when returned provenance explicitly says so.
3. If nothing matches, say it was not found in the business price list. If the user asks what other contractors charge, say this workflow only uses their own price list and has no market prices. Do not call `suggest_prices` or supply a market range from memory.
4. Answer in the user's language. Do not create or change items; direct changes to the Tofu app.
