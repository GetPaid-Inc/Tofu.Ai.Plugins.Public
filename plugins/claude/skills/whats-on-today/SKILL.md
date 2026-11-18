---
name: whats-on-today
description: Use when the user asks what is on the schedule today or this week, who is going where, or which visits are unassigned or overdue in their Tofu Field Service business.
---

# What is on today

1. Call `search_visits` with no arguments for today and seven days ahead. Use `from` and `to` for another window, `assigned` false for unassigned visits, or `worker_id` for one person. For today, retain only today's rows after converting their timestamps to the business timezone.
2. Use `period.timezone` to display `starts_at` and group days; do not group the UTC timestamp before conversion. If the business timezone is unknown, explicitly label times UTC. Do not infer a geographic timezone or daylight-saving rules from a UTC offset alone.
3. Group rows for the same job and start time, preserving every returned worker and visit id. Show client, job, status and assigned workers together, and explicitly mark unassigned visits. Call `get_team` only when a person's `user_id` is needed for `worker_id`. Do not infer team members absent from the results.
4. Mark `is_overdue` rows. For earlier overdue visits, pass an earlier `from`, `to` today and `statuses` ["scheduled"], then retain rows marked `is_overdue`. A window is at most 92 days.
5. A call returns up to 50 visits by default; use `page_size` 100 when needed. Follow `next_cursor` as `cursor` with the same filters to read the remaining visits. If `has_more` remains true without a usable cursor, narrow the dates. If even a single day is truncated, label the schedule incomplete rather than claiming everyone is listed.

An empty schedule is a normal answer. Answer in the user's language and never invent visits.
