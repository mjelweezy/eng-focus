# Running context — Make neno the source of truth for all bookkeeping
_Initiative: ce07f00e · maintained by the daily job + Matthew_
_Last updated: 2026-06-26_

## Decisions
- [2026-06-23] Aged-receivables analysis (by customer, 30/60/90/120+ day buckets) is a minimum AR reporting requirement. (source: Granola — Double-Entry Bookkeeping Open Questions)
- [2026-06-23] Q3 goal restated: 30 customers running on neno for bookkeeping, with neno as the single source of truth feeding Exact. (source: Granola — Q2 Retro & Q3 Planning)
- [2026-06-23] Intercompany interest auto-accrual deprioritised as a nice-to-have (currently tracked in Excel). (source: Granola — DP session)
- [2026-06-23] Depreciation review runs in July and annually for now; year-end balance correctness is the key requirement (monthly journals possible in Exact). (source: Granola — DP session)
- [2026-06-19] End-to-end AR reconciliation is now a tracked Linear project (lead David, Planned) — first concrete piece of this initiative.
- [2026-06-25] Three of the next-5 cohort run payroll that currently needs a manual monthly CSV import from Numbrs; payroll-integration viability for Q3 to be determined. (source: Granola/Slack - M&M week)

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
- (project: Depreciation & accruals) Material accruals discovered post-close (e.g. legal claims, missed intercompany interest) are handled via approval-gated, insert-only adjustment entries with a full audit log. (source: DP session, 23 Jun 2026)
- (project: Depreciation & accruals) Depreciation is grouped by asset type (not per item), each group with a purchase date and useful life; a fixed asset register lets accountants review schedules and verify depreciation isn't over-applied. (source: DP session, 23 Jun 2026)
- (project: Depreciation & accruals) Accruals book an expected expense when no invoice exists (especially at year-end); when the real invoice arrives the accrual is manually reversed and the actual expense booked. AI opportunity: detect a matching accrual on invoice arrival and offer one-step reversal. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Supports intercompany bookings; intercompany interest auto-accrual was deprioritised as a nice-to-have. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Every transaction with a related party must carry a tag/code identifying the counterparty entity (for statutory reporting, tax filings, intercompany reconciliation); GL-account drill-down must show the related party per line, for balance-sheet and P&L items. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) neno need not hold the books of related parties — only track money movement between the client entity and each named counterparty. (source: DP session, 23 Jun 2026)
- (project: End-to-end AR reconciliation) ~EUR 15K in outstanding receivables flagged with no active debtor management yet; AR end-to-end is a Q3 priority and needs a debtor-management view. (source: DP session, 23 Jun 2026)
- (project: Credit note processing (AR & AP)) Credit-note processing (both AR & AP) is a Q3 feature; still to be specced — likely intersects the GL period-close/correction rules. (source: Q3 planning, 23 Jun 2026)
- (project: Third-party wallet transaction import (MVP)) Needed so non-Swan banking customers can feed transactions into neno (bypassing the Swan requirement); start with Stripe, then additional channels. (source: DP session / Q3 planning, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Not covered in the 23 Jun DP session; requirements still to be defined. (source: DP session, 23 Jun 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-23] (Source: DP design session, 23 Jun 2026) Aged-receivables reporting (30/60/90/120+ buckets by customer) is a minimum requirement → captured on the Financial reporting project. Depreciation/accruals and intercompany interest-accrual notes captured on their respective projects; payroll not yet discussed.
