---
name: set-up-pricing
description: Set up a company's pricing in Homshi from nothing — a seed for its trade, the supplier's price list, a default rate card and template — so proposals price themselves. Use when the brief says the price book is empty, a rate card or template is missing, or the user asks how to start pricing.
arguments:
  - name: trade
    description: The kind of work, e.g. roofing, plumbing, handyman, marine, lawn. Optional — the brief usually says.
    required: false
homshi:
  tools: [company_brief, list_pricing_seeds, seed_pricing_method, import_price_list, set_price_feed, list_pricing_models, update_rate_card, list_proposal_templates, update_proposal_template, test_rate_card, save_catalog_item]
---
# Set up pricing

The goal: a proposal made from a lead prices itself — every line from the price book, every
price through the rate card, the tiers from the template — so nobody types a number.

## Before anything
1. `company_brief` with the company's id. Read the **Price book** line and **Next steps**. If the
   book already has items and a default card and template, stop: pricing is set up; offer
   `first-proposal` instead.
2. Say back which company you are setting up. Never set up pricing on the account level when the
   brief lists more than one company.

## Steps
1. **Seed the trade.** `list_pricing_seeds`, pick the seed for the trade ({trade} if given, else the
   brief's *Work* line, else ask). `seed_pricing_method` with that seed. A seed is a complete set —
   items, assemblies, a rate card with the method's rules, a template — and is idempotent: seeding
   twice adopts, it never duplicates.
2. **Their real costs.** Ask for the supplier's export (CSV or XLSX). `import_price_list` with
   `preview_only` first; read `matched`, `new`, `skipped`; then import for real. If the supplier
   publishes the file at a URL, `set_price_feed` with the URL and `daily|weekly|monthly` so it stays
   current — the sweep runs the same import.
3. **The card.** `list_pricing_models`; the seed's card is the default for its service. Confirm the
   markup, tax rule, minimum job and the *approval below* margin with the user; `update_rate_card`
   for changes. One default per service — `is_default_for_service`.
4. **The template.** `list_proposal_templates`; the seed's template is the default for its scope.
   If the company has more than one kind of work, one default per kind (`update_proposal_template`
   with `is_default_template`).
5. **Prove it.** `test_rate_card` on a draft proposal — the diff shows every line priced through
   the card, generated lines and what still `needs` confirming. Show the user the numbers.

## Rules
- Prices come from the book and the card. If a number is not in the book, it is a book item to
  add (`save_catalog_item`), not a line to type.
- Preview before every import; tell the user what moved and by how much before the real run.
- Company scoping: every call carries the company's id.

## Finish
Tell the user, in three lines: what was seeded, what the card charges (method, markup, minimum),
and that the next lead's proposal will build from the template — then offer `first-proposal`.
