---
name: first-proposal
description: Build a proposal for a lead the way Homshi prices it — from the template, through the rate card, with tiers — and hand it to the user to send. Use when the user asks for a quote, an estimate or a proposal for a lead or a job.
arguments:
  - name: lead
    description: The lead's name or id. Optional — ask if missing.
    required: false
homshi:
  tools: [company_brief, list_leads, create_proposal, get_proposal, get_proposal_scope, confirm_proposal_scope, insert_assembly, insert_options, apply_pricing_model, explain_price, request_price_approval]
---
# First proposal

## Before anything
1. `company_brief` for the company. If the book is empty or no default template exists, run
   `set-up-pricing` first — a proposal without a book is a typed number, and Homshi refuses those.
2. `list_leads` to resolve {lead} to an id (search by name). Read the lead's scope: what it says,
   and what is *unverified* — an AI receptionist's or an email's extraction prices nothing until
   the estimator confirms it.

## Steps
1. `create_proposal` with `lead_id` and the company's id. Homshi builds it from the template the
   lead's work resolves to; the answer's `template` says which, what was inserted, and what it
   still `needs`.
2. If `needs` names fields (squares, dock length, hours…): `get_proposal_scope`, then either
   `confirm_proposal_scope` for values the lead already carries (the report, the customer's word,
   now confirmed by you *only if the user confirms them*) or ask the user for the value.
3. Options: if the user wants choices, `insert_options` — one assembly per tier (Good / Better /
   Best), each priced by the card; nothing hand-priced.
4. `apply_pricing_model` with `preview_only` to see the reprice diff; read the warnings and the
   approval flag; then apply.
5. `explain_price` on any line the user questions — the card, the rule, the cost it came from.
6. If the margin falls below the card's floor, `request_price_approval` names the approver;
   do not try to send.

## Rules
- Never create a job to make a proposal; a proposal can start from a lead or on its own.
- Never type a price. A missing item is a book item; a discount is the card's rule or an approved
  override, never an edited line.
- Nothing here sends. The proposal waits in Sales → Proposals for the user to read and send.

## Finish
Report: the proposal number, the total (and per-tier totals), what was confirmed and what still
needs the estimator, and that it is waiting to be sent from Homshi.
