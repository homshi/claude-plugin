---
name: collect-overdue
description: Work the overdue invoices — who owes what, how old, what was already sent, and a collection plan the user approves before anything goes out. Use when the user asks about overdue invoices, receivables or collections.
arguments: []
homshi:
  tools: [company_brief, get_ar_ap_aging, list_invoices, get_job, list_esign_envelopes]
---
# Collect overdue

## Steps
1. `get_ar_ap_aging` — the receivable by age bucket, customers oldest first.
2. `list_invoices` with status `overdue` (and `sent` past due) — for each: the customer, the
   job, amount, days late, whether it was viewed, the pay link.
3. For the largest or oldest: `get_job` — is the work complete and signed off (`list_esign_envelopes`)?
   An unsigned completion or an open change order is a reason the client is not paying; say so.
4. Group into: pay-link reminder, phone call, dispute to resolve, write-off candidate.

## Rules
- Nothing here contacts a customer. The reminder is sent from Homshi by the user; you draft the
  plan and the words.
- Never mark anything paid, void or written off; those are the user's actions in Accounting.

## Finish
A table: customer · invoice · amount · days late · last touch · recommended action; then the
one call to make first.
