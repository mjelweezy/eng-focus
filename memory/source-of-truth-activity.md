# Running context — Source of truth for all bookkeeping activity
_Initiative: b508d2b3-f876-4068-beec-e3c9899dd8c4 · maintained by the daily job + Matthew_
_Last updated: 2026-07-30_

> Split out of `source-of-truth.md` (initiative ce07f00e) on 30 Jul 2026. Covers the
> accountant-performed bookkeeping actions: AR reconciliation, credit notes, accruals,
> depreciation, related parties, financial reporting, corrections, inter-company payments, plus
> adjacent platform features (team permissions, customer projects, bug-fixes). See
> `source-of-truth-data.md` for the external data integrations feeding this work. Full pre-split
> history lives in the archived `source-of-truth.md`.

## Decisions
- [2026-06-23] (carried forward) Aged-receivables analysis (by customer, 30/60/90/120+ day buckets) is a minimum AR reporting requirement. (source: Granola — Double-Entry Bookkeeping Open Questions)
- [2026-06-23] (carried forward) Q3 goal restated: 30 customers running on neno for bookkeeping, with neno as the single source of truth feeding Exact. (source: Granola — Q2 Retro & Q3 Planning)
- [2026-06-23] (carried forward) Intercompany interest auto-accrual deprioritised as a nice-to-have (currently tracked in Excel). (source: Granola — DP session)
- [2026-06-23] (carried forward) Depreciation review runs in July and annually for now; year-end balance correctness is the key requirement (monthly journals possible in Exact). (source: Granola — DP session)
- [2026-06-19] (carried forward) End-to-end AR reconciliation is a tracked Linear project — now In Progress (lead Joel).
- [2026-07-06] (carried forward, Matthew) Split 'Depreciation & accruals' into two projects: 'Depreciation schedules' and 'Accruals'.
- [2026-07-07] (carried forward, Matthew) Depreciation schedules and credit note processing deprioritised for July - moved to Later on the board and Backlog in Linear.
- [2026-07-30] (Matthew) Initiative split into 'bookkeeping data' vs 'bookkeeping activity'; this file covers the accountant-performed actions. AR reconciliation is now In Progress (Joel) - promoted to the "now" bucket.

## Open questions
- [open] (carried forward) Full reporting requirements list still being compiled by DP. (project: Financial reporting)
- [open] (carried forward) Feature sequencing and ownership for the post-GL bookkeeping scope not yet decided. (owner: Matthew)
- [open] (carried forward) Ocean Ionics Espana: separate entity or a second bank account? Booking treatment (intercompany vs investment) depends on the answer. (source: Granola — DP session)
- [open] (carried forward) VAT filing period flexibility (monthly/quarterly/bi-monthly) must be configurable per customer and country. (project: Financial reporting) (source: Granola — DP session)
- [open] (carried forward) Accountant portfolio management (per group/entity): where should it live (Yaroslav proposes Atlas) and what data source backs it? (source: Slack #accounting-mvp, 14 Jul)
- [open] (carried forward) Accept hybrid data and a longer Exact dependence for more customers in order to prioritise spend-management, or hold the line on book-keeping completeness first? (owner: Matthew) (source: Slack #advisory-services, 16 Jul)
- [open] (carried forward) Which two upcoming book-keeping features/integrations are prioritised first, and what are their requirements? (owner: Matthew) (source: Slack #core-team, 28 Jul)

## Risks
- [med] (carried forward) Scope is broad and unsequenced; nothing staffed yet beyond AR reconciliation.
- [med] (carried forward) Full reporting requirements not yet enumerated — scope could grow once DP's list lands. (project: Financial reporting)
- [med] (carried forward) ~EUR 15K in outstanding receivables flagged with no active debtor management yet. (project: End-to-end AR reconciliation) (source: Granola — DP session)

## Next steps
- [carried forward] DP to compile the full reporting requirements list. (owner: DP, ASAP) (project: Financial reporting)
- [carried forward] Define and file the remaining projects after AR reconciliation. (owner: Matthew)
- [2026-07-28] (carried forward) Sync with Matthew on the end-to-end AR surfaces (PR #1232) to confirm they meet the requirements before building further. (owner: Joel/Matthew) (source: Slack #core-team, 28 Jul)

## Projects (filed in Linear)
- [2026-07-30] Attached to this new initiative: Financial reporting, Credit note processing (AR & AP), Related-parties register, Depreciation schedules, Accruals, Native team features & permissions, Customer project creation & management, Bookkeeping bug-fixes, End-to-end AR reconciliation. New backlog items from the Q3 roadmap deck not yet filed as Linear projects: Investment & loan booking, Corrections/memorandums, Inter-company payments, Backfill bookings to AGL, Opening balances for AGL.

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Financial reporting) Aged-receivables analysis by customer in 30/60/90/120+ day buckets — minimum reporting requirement. (source: DP session, 23 Jun 2026)
- (project: Financial reporting) Full reporting requirements list (100+ items) pending from DP; expand this project when it lands. (source: DP session, 23 Jun 2026)
- (project: Financial reporting) Minimum reporting set: trial balance; full GL export; P&L; balance sheet; aged receivables by customer (30/60/90/120+); fixed asset register with depreciation rates per asset; drill-down export for any individual GL account. (source: DP session, 23 Jun 2026)
- (project: Financial reporting) VAT reporting broken down by rate and territory (21%/9%/0% Dutch, EU sales, non-EU sales; same for purchases); VAT export mapped to Nextens. (source: DP session, 23 Jun 2026)
- (project: Accruals) Material accruals discovered post-close are handled via approval-gated, insert-only adjustment entries with a full audit log. (source: DP session, 23 Jun 2026)
- (project: Depreciation schedules) Depreciation is grouped by asset type (not per item), each group with a purchase date and useful life; a fixed asset register lets accountants review schedules and verify depreciation isn't over-applied. (source: DP session, 23 Jun 2026)
- (project: Accruals) Accruals book an expected expense when no invoice exists; when the real invoice arrives the accrual is manually reversed and the actual expense booked. AI opportunity: detect a matching accrual on invoice arrival and offer one-step reversal. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Supports intercompany bookings; intercompany interest auto-accrual deprioritised as a nice-to-have. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Every transaction with a related party must carry a tag/code identifying the counterparty entity; GL-account drill-down must show the related party per line. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) neno need not hold the books of related parties — only track money movement between the client entity and each named counterparty. (source: DP session, 23 Jun 2026)
- (project: End-to-end AR reconciliation) ~EUR 15K in outstanding receivables flagged with no active debtor management yet; AR end-to-end is a Q3 priority and needs a debtor-management view. (source: DP session, 23 Jun 2026)
- (project: End-to-end AR reconciliation) Reconciliation-suggestion constraints must carry over to AR: at most one active suggestion per invoice and per transaction, and trustworthy 'not matched' / 'needs review' lists. (source: Slack #accounting-mvp (Ihor), 7 Jul 2026)
- (project: Credit note processing (AR & AP)) Credit-note processing (both AR & AP) is a Q3 feature; still to be specced — likely intersects the GL period-close/correction rules. (source: Q3 planning, 23 Jun 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._
- [2026-07-16] (carried forward) Expose invoice/quote operations via an MCP server/API plus trustworthy non-reconciled-items / missing-documents lists for external agent use - could belong to End-to-end AR reconciliation, invoicing, or a new API/MCP project; needs Matthew's attribution. (source: Granola/tldv - Sil x Yaroslav API call, 15 Jul)
- [2026-07-16] (carried forward, update) The prospective first MCP-API test customer (Sil) declined; the invoice/quote MCP requirement stands for future founder/developer customers and still needs Matthew's attribution. Yaroslav is drafting a Neno MCP v1 scope (Invoices, Quotes, Bills). (source: Slack #product, 16 Jul)
- [2026-07-28] (carried forward) The admin reconciliation queue needs date filtering, server-side search and sortable Date/Amount columns. Filed as NEO-1602 (Art) on the "Reconciliation" project, which sits outside the tracked initiatives; needs Matthew's attribution. (source: Linear NEO-1602, 28 Jul)
- [2026-07-27] (carried forward) Surface a typical GL-account mapping per vendor at bill-coding recommendation time, to reduce Andries's per-invoice manual vendor-context lookups. Discussed as a near-term addition to the Smart Bill Review coding assistant, which sits outside the tracked initiatives; needs Matthew's attribution. (source: Granola - Andries and Art, 27 Jul)

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-23] (carried forward, Source: DP design session, 23 Jun 2026) Aged-receivables reporting (30/60/90/120+ buckets by customer) is a minimum requirement → captured on the Financial reporting project.
