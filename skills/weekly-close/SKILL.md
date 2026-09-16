---
name: weekly-close
description: The owner's weekly close — money in and out, what is waiting on a signature or an approval, the week ahead, and the three actions that matter. Use on a Friday or whenever the user asks how the business is doing.
arguments: []
homshi:
  tools: [company_brief, get_financial_summary, get_cashflow, get_ar_ap_aging, get_cashflow_forecast, list_proposals, list_esign_envelopes, get_schedule, get_wip]
---
# Weekly close

## Steps
1. `company_brief` — the pipeline line is the frame: open leads, drafts, proposals out, active
   jobs, receivable and overdue.
2. Money: `get_financial_summary`, `get_cashflow`, `get_ar_ap_aging` (who owes, oldest first),
   `get_cashflow_forecast` (flag any of the next 13 weeks that goes negative).
3. Work: `get_wip` — jobs over- or under-billed against their percent complete.
4. Waiting: `list_proposals` with status `sent` (out and unanswered — nudge candidates),
   `list_esign_envelopes` with status `sent` (unsigned).
5. Ahead: `get_schedule` for the next 7 days — anyone double-booked or idle, anything unassigned.

## Rules
- Numbers first, one screen. Every figure names its source (the tool).
- Do not send nudges or reminders yourself; name them as actions for the user.

## Finish
End with the three actions you would take this week, each tied to a number above.
