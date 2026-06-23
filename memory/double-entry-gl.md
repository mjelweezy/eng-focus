# Running context — Enable VAT submissions via double-entry GL
_Initiative: fef38f90 · maintained by the daily job + Matthew_
_Last updated: 2026-06-23_

## Decisions
- [2026-06-22] Insert-only ledger architecture with reversals — no direct edits to journal entries; corrections reverse and rebook. (source: Granola — Next Steps AGL with Mark)
- [2026-06-22] Period closes define immutability — open periods allow free reversals/rebookings; closed periods take new adjustment entries only (month/quarter/year). (source: Granola — Next Steps AGL)
- [2026-06-22] Monitoring over rollback — accountant review UI is the priority, not complex rollback mechanics. (source: Granola — Next Steps AGL)
- [2026-06-22] Euro-only for now; multi-currency deferred but architecture shouldn't preclude it. (source: Granola — Next Steps AGL)
- [2026-06-22] Q3 target: VAT submission from neno for 6 customers (AR & AP); opening balance from the Q1/Q2 Exact close; backfilling deferred unless it risks the VAT outcome. (source: Granola — Next Steps AGL)
- [2026-06-23] VAT corrections after a period close are booked in the next period (dated day 1); amounts under EUR 1,000 fold into the next return without a supplemental filing. Balance sheet needs three VAT lines: receivable, payable, corrections/suspense. (source: Granola — Double-Entry Bookkeeping Open Questions)
- [2026-06-23] Closed periods lock writes by default; unlocking is approval-gated and only for material post-close accruals; insert-only with full audit log. (source: Granola — DP session)
- [2026-06-23] Multi-currency: store foreign amount + transaction-date rate, derive euro on demand; month-end revaluation of FX assets/liabilities to an unrealized FX gains/losses account (P&L under Dutch GAAP, equity under IFRS). (source: Granola — DP session)
- [2026-06-23] VAT reporting must break down by rate and territory: 21% / 9% / 0% (Dutch), EU sales, non-EU sales — and the same for purchases; VAT export mapped to Nextens for submission. (source: Granola — DP session)

## Open questions
- [open] Belgium gapless-ledger requirement — does it constrain day-to-day ledger architecture or only closed-period exports/reporting? Not resolved in the 23 Jun session. (source: Granola — DP session)
- [open] Full reporting requirements list being compiled by DP (potentially 100+ items) — will frame future design. (owner: DP)
- [open] What must change in the current system to use double-entry bookkeeping for the Q3 VAT submission?
- [open] VAT filing period must be configurable per customer/country (monthly, quarterly, or bi-monthly). (source: Granola — DP session)
- [resolved 2026-06-23] How do VAT corrections work when a period is closed? → next period, with <EUR 1,000 folded in.
- [resolved 2026-06-23] Edit permissions for humans vs agents? → closed periods lock; approval-gated insert-only with audit log.
- [resolved 2026-06-23] Multi-currency FX handling? → store rate at txn date; month-end revaluation to unrealized FX account.

## Risks
- [high] Spike code (~13k lines, Claude-generated) took liberties with DB writes; atomicity and no-overlapping-bookings must be guaranteed before productionising. Review under way this week (Mark/Matthew). (source: Granola — Next Steps AGL)
- [med] Belgium gapless-ledger scope unconfirmed.
- [med] DP's full reporting requirements list not yet compiled — could expand GL scope.

## Next steps
- [2026-06-23] DP to compile full reporting requirements list. (owner: DP, due ASAP)
- [2026-06-23] Matthew to schedule the follow-up design session (~1 week). (owner: Matthew)
- [2026-06-23] Compile outstanding open questions before the follow-up. (owner: Matthew / Mark)
- Review spike code for atomicity, security, correctness. (owner: Mark + Matthew, this week)
- Reproduce the balance check in production with periods. (owner: Engineering, by 25 Jun)
- Map the VAT export to Nextens for submission. (owner: TBD, Q3)

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project (this project is In Progress, so they are posted as a proposed comment, not auto-applied)._
- (project: Start writing to neno's double-entry GL) Insert-only ledger with reversals — no edits to journal entries; corrections reverse and rebook. (source: Granola — Next Steps AGL, 22 Jun 2026)
- (project: Start writing to neno's double-entry GL) Period closes define immutability; closed periods lock writes by default; unlocking is approval-gated, insert-only, and fully audited. (source: Granola — DP session, 23 Jun 2026)
- (project: Start writing to neno's double-entry GL) VAT: corrections after close booked in the next period (<EUR 1,000 folds in); balance sheet carries three VAT lines (receivable, payable, corrections/suspense); breakdown by rate/territory; export to Nextens. (source: Granola — DP session, 23 Jun 2026)
- (project: Start writing to neno's double-entry GL) Multi-currency: store foreign amount + transaction-date rate, derive euro on demand; month-end revaluation of FX assets/liabilities to an unrealized FX gains/losses account. (source: Granola — DP session, 23 Jun 2026)

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-23] Agentic-ledger idea: when a backdated entry is posted, automatically detect which reports are affected and surface the delta. (source: Granola — DP session)
