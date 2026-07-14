# Running context — Make neno the source of truth for all bookkeeping
_Initiative: ce07f00e · maintained by the daily job + Matthew_
_Last updated: 2026-07-14_

## Decisions
- [2026-06-23] Aged-receivables analysis (by customer, 30/60/90/120+ day buckets) is a minimum AR reporting requirement. (source: Granola — Double-Entry Bookkeeping Open Questions)
- [2026-06-23] Q3 goal restated: 30 customers running on neno for bookkeeping, with neno as the single source of truth feeding Exact. (source: Granola — Q2 Retro & Q3 Planning)
- [2026-06-23] Intercompany interest auto-accrual deprioritised as a nice-to-have (currently tracked in Excel). (source: Granola — DP session)
- [2026-06-23] Depreciation review runs in July and annually for now; year-end balance correctness is the key requirement (monthly journals possible in Exact). (source: Granola — DP session)
- [2026-06-19] End-to-end AR reconciliation is now a tracked Linear project (lead David, Planned) — first concrete piece of this initiative.
- [2026-06-25] Three of the next-5 cohort run payroll that currently needs a manual monthly CSV import from Numbrs; payroll-integration viability for Q3 to be determined. (source: Granola/Slack - M&M week)

- [2026-07-06] (Matthew) Split 'Depreciation & accruals' into two projects: 'Depreciation schedules' (Planned - committed for July) and 'Accruals' (Backlog - not committed). Requirements retagged accordingly.

- [2026-07-07] (Matthew) Depreciation schedules and credit note processing are deprioritised for July - moved back to Later on the board and to Backlog in Linear. Note: Andries asked (6 Jul) for a depreciation schedule from w/c 7 Jul; deprioritised regardless.

- [2026-07-06] OI duplicate bank transactions fixed (NEO-1448, Mark, Bookkeeping bug-fixes); the durable fix would be NEO-1299 (pull bank transactions from Exact and suppress already-booked ones). (source: Linear / Slack #accounting-mvp, 6 Jul)
- [2026-07-07] Reconciliation suggestions are now limited to one active suggestion per bill and per transaction (NEO-1451, Ihor, shipped 7 Jul) - fixes bills appearing multiple times in the queue. Ihor flagged the same constraint will likely be needed for AR reconciliation once it exists. (source: Linear NEO-1451 / Slack #accounting-mvp, 7 Jul)
- [2026-07-07] Workflow agreed: once the 'Not matched' and 'Needs your review' lists are trustworthy (Mark/Ihor, by EOD 7 Jul), Andries reviews the ~55 not-matched transactions and triggers missing-bill tasks for Marloes. (source: Slack #accounting-mvp, 7 Jul)

- [2026-07-08] Reconciliation review state: all bills/transactions are now properly surfaced in the app (Ihor shared a review artifact for Andries/Joel); some minor DB anomalies still under investigation. The duplicate-entry fix was reviewed by Mark, who caught 2-3 issues, all resolved. (source: Slack #accounting-mvp / Granola - Daily stand-up, 8 Jul)
- [2026-07-09] NEO-1464 filed (Ihor): bills can accept reconciliation links while still NEEDS_REVIEW, hiding them from the extraction-review list and permitting reconciliation (and Exact sync) before extraction approval. Invariant to enforce: a bill must be extraction-approved (REVIEWED) before reconciliation; the legacy APPROVED bill status is to be removed. Ihor flagged it on his last day before summer holiday (10 Jul); Yaroslav to prioritise next week unless Joel gets to it sooner. (source: Linear NEO-1464 / Slack #tech-team, 10 Jul)
- [2026-07-08] Per the stand-up notes: Swan transactions are syncing into Xero for 3 workspaces via the per-workspace connections pipeline, and 163 backlog Q2 invoices were bulk-uploaded via a Claude-assisted harness; flagged that the invoice/billing flow needs a proper fix before customer count scales. (source: Granola - Daily stand-up, 8 Jul)
- [2026-07-13] The admin area and Atlas now run together on a separate domain (prod atlas.neno.co, sandbox atlas.neno.build); Yaroslav shared how devs should test the Atlas admin experience. (source: Slack #tech-team (Yaroslav), 13 Jul)
- [2026-07-13] Stand-up recap: a direct Exact connection for transactions/synchronisation is established, all invoices for existing customers are scheduled and verified correct, and accountant engagements are tracked by entity, group and larger groups (recap wording is low-fidelity). (source: Slack #tldv-channel - daily stand-up recap (tldv), 13 Jul)

## Open questions
- [open] Payroll design not yet discussed — open design area for a future session.
- [open] Full reporting requirements list still being compiled by DP.
- [open] Feature sequencing and ownership for the post-GL bookkeeping scope not yet decided. (owner: Matthew)
- [open] Ocean Ionics Espana: separate entity or a second bank account? Booking treatment (intercompany vs investment) depends on the answer. (source: Granola — DP session)
- [open] VAT filing period flexibility (monthly/quarterly/bi-monthly) must be configurable per customer and country. (source: Granola — DP session)

## Risks
- [med] Scope is broad and unsequenced; nothing staffed yet beyond AR reconciliation (David).
- [med] Full reporting requirements not yet enumerated — scope could grow once DP's list lands.
- [med] ~EUR 15K in outstanding receivables flagged with no active debtor management yet. (source: Granola — DP session)

## Next steps
- DP to compile the full reporting requirements list. (owner: DP, ASAP)
- Define and file the remaining projects after AR reconciliation. (owner: Matthew)

## Projects (filed in Linear)
- [2026-06-23] Generated the initiative's feature set as Linear projects (Backlog), attached to the initiative, with summaries + DP-sourced requirements where available: Financial reporting, Credit note processing (AR & AP), Related-parties register, Payroll (Numbrs), Third-party wallet transaction import, Depreciation & accruals, Native team features & permissions, Customer project creation & management. End-to-end AR reconciliation already existed (David, Planned).
- Requirements practice for now: update the Linear project **summary/description** directly when new requirements surface, marking the source. Future: append as project comments instead.

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Financial reporting) Aged-receivables analysis by customer in 30/60/90/120+ day buckets — minimum reporting requirement. (source: DP session, 23 Jun 2026)
- (project: Financial reporting) Full reporting requirements list (100+ items) pending from DP; expand this project when it lands. (source: DP session, 23 Jun 2026)
- (project: Financial reporting) Minimum reporting set: trial balance; full GL export (all accounts with detailed transaction lines); P&L; balance sheet; aged receivables by customer (30/60/90/120+); fixed asset register with depreciation rates per asset; drill-down export for any individual GL account. (source: DP session, 23 Jun 2026)
- (project: Financial reporting) VAT reporting broken down by rate and territory (21%/9%/0% Dutch, EU sales, non-EU sales; same for purchases); VAT export mapped to Nextens. (source: DP session, 23 Jun 2026)
- (project: Accruals) Material accruals discovered post-close (e.g. legal claims, missed intercompany interest) are handled via approval-gated, insert-only adjustment entries with a full audit log. (source: DP session, 23 Jun 2026)
- (project: Depreciation schedules) Depreciation is grouped by asset type (not per item), each group with a purchase date and useful life; a fixed asset register lets accountants review schedules and verify depreciation isn't over-applied. (source: DP session, 23 Jun 2026)
- (project: Accruals) Accruals book an expected expense when no invoice exists (especially at year-end); when the real invoice arrives the accrual is manually reversed and the actual expense booked. AI opportunity: detect a matching accrual on invoice arrival and offer one-step reversal. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Supports intercompany bookings; intercompany interest auto-accrual was deprioritised as a nice-to-have. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Every transaction with a related party must carry a tag/code identifying the counterparty entity (for statutory reporting, tax filings, intercompany reconciliation); GL-account drill-down must show the related party per line, for balance-sheet and P&L items. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) neno need not hold the books of related parties — only track money movement between the client entity and each named counterparty. (source: DP session, 23 Jun 2026)
- (project: End-to-end AR reconciliation) ~EUR 15K in outstanding receivables flagged with no active debtor management yet; AR end-to-end is a Q3 priority and needs a debtor-management view. (source: DP session, 23 Jun 2026)
- (project: Credit note processing (AR & AP)) Credit-note processing (both AR & AP) is a Q3 feature; still to be specced — likely intersects the GL period-close/correction rules. (source: Q3 planning, 23 Jun 2026)
- (project: Third-party wallet transaction import (MVP)) Needed so non-Swan banking customers can feed transactions into neno (bypassing the Swan requirement); start with Stripe, then additional channels. (source: DP session / Q3 planning, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Not covered in the 23 Jun DP session; requirements still to be defined. (source: DP session, 23 Jun 2026)

- (project: End-to-end AR reconciliation) Reconciliation-suggestion constraints must carry over to AR: at most one active suggestion per invoice and per transaction, and trustworthy 'not matched' / 'needs review' lists so accountants can trigger missing-document tasks. (source: Slack #accounting-mvp (Ihor), 7 Jul 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-23] (Source: DP design session, 23 Jun 2026) Aged-receivables reporting (30/60/90/120+ buckets by customer) is a minimum requirement → captured on the Financial reporting project. Depreciation/accruals and intercompany interest-accrual notes captured on their respective projects; payroll not yet discussed.
