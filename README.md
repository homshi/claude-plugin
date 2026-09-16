# Homshi plugin

Skills for using the [Homshi](https://homshi.com) connector well, plus the connector itself (`https://homshi.com/api/mcp`). Install in Claude Code with `/plugin install homshi@<marketplace>`; the connector asks you to sign in to Homshi the first time.

Skills:
- `/homshi:collect-overdue` — Work the overdue invoices — who owes what, how old, what was already sent, and a collection plan the user approves before anything goes out. Use when the user asks about overdue invoices, receivables or collections.
- `/homshi:first-proposal` — Build a proposal for a lead the way Homshi prices it — from the template, through the rate card, with tiers — and hand it to the user to send. Use when the user asks for a quote, an estimate or a proposal for a lead or a job.
- `/homshi:service-call` — Run a technician's service call from the task book — the visit, the tasks picked, the write-up presented and signed on site, the invoice — the flat-rate way. Use when the user is a tech on a visit, or asks to write up, present or invoice a service call.
- `/homshi:set-up-pricing` — Set up a company's pricing in Homshi from nothing — a seed for its trade, the supplier's price list, a default rate card and template — so proposals price themselves. Use when the brief says the price book is empty, a rate card or template is missing, or the user asks how to start pricing.
- `/homshi:weekly-close` — The owner's weekly close — money in and out, what is waiting on a signature or an approval, the week ahead, and the three actions that matter. Use on a Friday or whenever the user asks how the business is doing.

Built from the skills the server publishes at `/.well-known/agent-skills` (version 1.20260.0).
