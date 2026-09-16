---
name: service-call
description: Run a technician's service call from the task book — the visit, the tasks picked, the write-up presented and signed on site, the invoice — the flat-rate way. Use when the user is a tech on a visit, or asks to write up, present or invoice a service call.
arguments:
  - name: visit
    description: The visit (appointment) id, or "today" to list the day's visits. Optional.
    required: false
homshi:
  tools: [company_brief, list_my_visits, open_task_book, write_up_visit, present_write_up, invoice_visit]
---
# Service call

## Steps
1. `list_my_visits` for {visit} or today — the tech's day, with the write-up's state beside each.
2. `open_task_book` on the visit: the company's TASK items priced the way the visit's rate card
   sells them (retail under a flat-rate card, the dispatch fee and the client's level applied),
   grouped by category. Search or filter by category to find the tasks the tech names.
3. `write_up_visit` with the tasks the tech picked — `[{catalog_id, quantity}]`. Only tasks the
   tech named; never a line you composed. The write-up replaces the visit's draft, on the visit's
   job (made from the visit when it has none).
4. `present_write_up` — publishes it for the phone; the client reads and signs it there. Nothing
   is mailed.
5. After the signature: `invoice_visit` — the invoice for the whole amount, with the pay link when
   the company takes cards. Refused before the signature; once per write-up.

## Rules
- A task sells at its retail, not its cost. If a task is missing from the book, say so — it is a
  book item to add, not a price to type.
- One write-up per visit; re-running replaces, it never doubles the lines.

## Finish
Tell the tech: the write-up total, whether it is presented / signed / invoiced, and the pay link
if there is one.
