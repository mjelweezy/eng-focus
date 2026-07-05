# Running context — Enable VAT submissions via double-entry GL
_Initiative: fef38f90 · maintained by the daily job + Matthew_
_Last updated: 2026-07-05_

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
- [2026-06-26] Native double-entry GL (NEO-1361) is now IMPLEMENTED and covered by green tests on the build branch, gated behind an off-by-default feature flag pending production go-live; this supersedes the earlier dual-write spike that mirrored Exact's codes. Neno owns the chart of accounts and VAT codes; Exact becomes a removable downstream sync. (source: PR #1128 knowledgebase - General Ledger domain)
- [2026-06-26] Ledger architecture: every accounting action emits a neno event; a reliable booking engine turns each event into a balanced, VAT-aware journal entry in Neno's own chart, carrying counterparty and VAT-code dimensions; each entry references its event + source document; corrections are append-only contra entries (no edits/deletes). (source: PR #1128 knowledgebase)
- [2026-06-26] In scope for this build (TC-LEDGER-01..06 / INV-LEDGER-01..13, now 'Holds'): a correct and filable VAT return from Neno's own data; live and complete cash; VAT filing that survives Exact being disconnected; books that always trial-balance to zero; a tamper-evident append-only audit trail; drill-down by vendor / GL account / VAT code. (source: PR #1128 knowledgebase)
- [2026-06-26] VAT is a first-class dimension: every taxable line carries a VAT code on both the base and the tax line; the code's treatment (domestic / reverse-charge / intra-EU / import / export) drives the posting shape; the VAT return is a report mapping codes to boxes, validated against a real filed Dutch return (Happy Team Apps Q1 2026). (source: PR #1128 knowledgebase)
- [2026-06-25] 'Source of truth' reworded to 'Neno is the source of truth with regards to VAT filing' - scoped deliberately to avoid scope creep from external payment sources. (source: Granola - M&M)
- [2026-06-25] Confirmed: book ledger entries when bank transactions are imported (not only bills/invoices), so the bank balance is knowable before reconciliation completes (cash completeness via a suspense account). (source: Granola - M&M)
- [2026-06-25] Supplemental changes live in future reporting only; break-the-glass retroactively fixes reporting. (source: Granola - M&M)
- [2026-06-25] To track account balances at go-live, either a backfill or a cutoff booking (opening balances) is required. (source: Granola - M&M)
- [2026-06-25] Euro-only for now; XBRL statutory filing to be added later. (source: Granola - M&M)

- [2026-06-26] GL status (Mark): the design is locked and a first implementation is drafted with passing unit tests, but the native engine has NOT yet been run against real production data - next step is feeding real prod data through it in dev, which may surface code or even architecture changes. Still the architecture/spike phase. (source: Linear project status update, 26 Jun / edited 29 Jun)
- [2026-06-30] FX rate on a bill is booked at the ECB daily reference (mid) rate on the transaction date, frozen on the line; when the settling bank payment clears at a different rate the residual is a realised FX gain/loss posted to a dedicated FX-difference account, and any separate bank FX fee books to bank charges (not reconciled to a specific payment). (source: Granola - DP/Mark open questions neno GL, 30 Jun; Slack #accounting-mvp, 1 Jul)
- [2026-06-30] FX representation (INV-LEDGER-23, proposed): every journal line stores its native-currency amount + the transaction-date rate; the reporting-currency value is derived, never stored alone. Multi-currency balancing is split out to INV-LEDGER-27 (proposed): an entry may carry more than one currency and balances on reporting-currency value; INV-LEDGER-01 is reworded so balance = signed sum of reporting-currency values (stays 'Holds'). (source: Slack #accounting-mvp, 1 Jul)
- [2026-06-30] FX revaluation (INV-LEDGER-16, deferred) model decided: balance-sheet accounts only (P&L never revalued), revalue to the period-end rate, true-up booked to the FX result account; first practical case is USD bank accounts, run on demand. Out of scope for now, but rates are stored so it can be built later. (source: Slack #accounting-mvp, 1 Jul)
- [2026-06-30] Locked-period corrections: correct-forward is the default; restating a closed period is the exception, gated by a break-the-glass unlock (deliberate, non-default, per-workspace approver, full audit log, alert-all with amount-threshold escalation); prompt when a correction hits an already-filed period. (source: Granola - DP/Mark, 30 Jun; Slack #accounting-mvp, 1 Jul)
- [2026-06-30] VAT corrections are always corrected forward (closed books are never reopened for VAT); <EUR 1,000 net/year rolls into the next return, >EUR 1,000 goes on a supplementary return. The chart of accounts needs two VAT balance-sheet accounts - a normal VAT account and a corrections/control account; once the EUR 1,000 cumulative threshold is crossed all subsequent corrections (even small ones) route to the corrections account, which is empty again once the suppletie is filed. (source: Granola - DP/Mark, 30 Jun; Slack #accounting-mvp, 1 Jul)

## Open questions
- [open] Belgium gapless-ledger requirement — does it constrain day-to-day ledger architecture or only closed-period exports/reporting? Not resolved in the 23 Jun session. (source: Granola — DP session)
- [open] Full reporting requirements list being compiled by DP (potentially 100+ items) — will frame future design. (owner: DP)
- [resolved 2026-06-26] What must change in the current system to use double-entry bookkeeping for the Q3 VAT submission? -> Neno's native double-entry GL is now built and green-tested behind an off-by-default feature flag (NEO-1361, PR #1128); production go-live (opening balances/backfill + Exact decoupling) is the remaining step.
- [open] VAT filing period must be configurable per customer/country (monthly, quarterly, or bi-monthly). (source: Granola — DP session)
- [resolved 2026-06-23] How do VAT corrections work when a period is closed? → next period, with <EUR 1,000 folded in.
- [resolved 2026-06-23] Edit permissions for humans vs agents? → closed periods lock; approval-gated insert-only with audit log.
- [resolved 2026-06-23] Multi-currency FX handling? → store rate at txn date; month-end revaluation to unrealized FX account.
- [open] Year-end roll-forward (TC-LEDGER-15): closing income/expense into retained earnings with a clean new-year P&L and correct opening balance sheet - flagged CORE but still needs sign-off with DP. (owner: Mark/Matthew) (source: Granola - M&M, 25 Jun)

- [resolved 2026-06-30] Which FX rate when a bill and its settling transaction don't match? -> ECB mid rate at booking (frozen on the line), residual to a dedicated realised FX gain/loss account, bank FX fees a separate expense line.
- [open] FX balance rule not finally chosen: 'signed sum zero in the entry's one currency' (spike model) vs 'signed sum of reporting-currency values is zero' (native multi-currency); also confirm the full residual account set (FX difference, rounding, payment difference, discount). (owner: Design/DP) (source: Slack #accounting-mvp, 1 Jul)
- [open] Locked-period break-the-glass details: who approves, what is recorded, and whether the original filing must be resubmitted - not finalised (depends on future customer profile/risk); design the audit log + Slack unlock alerting (start by reporting all changes, add amount-based thresholds once noisy). (owner: Mark/DP) (source: Slack #accounting-mvp, 1 Jul)

## Risks
- [high] Spike code (~13k lines, Claude-generated) took liberties with DB writes; atomicity and no-overlapping-bookings must be guaranteed before productionising. Review under way this week (Mark/Matthew). (source: Granola — Next Steps AGL)
- [med] Belgium gapless-ledger scope unconfirmed.
- [med] DP's full reporting requirements list not yet compiled — could expand GL scope.
- [low] Native GL build (NEO-1361, PR #1128) landed green-tested behind an off-by-default flag; risk shifts from spike-code correctness to the production go-live cutover (opening-balance backfill/cutoff and Exact decoupling). (source: PR #1128)

## Next steps
- [2026-06-23] DP to compile full reporting requirements list. (owner: DP, due ASAP)
- [2026-06-23] Matthew to schedule the follow-up design session (~1 week). (owner: Matthew)
- [2026-06-23] Compile outstanding open questions before the follow-up. (owner: Matthew / Mark)
- Review spike code for atomicity, security, correctness. (owner: Mark + Matthew, this week)
- Reproduce the balance check in production with periods. (owner: Engineering, by 25 Jun)
- Map the VAT export to Nextens for submission. (owner: TBD, Q3)
- [2026-06-25] Mark to finish and send the truth-conditions document. (owner: Mark) (source: Granola - M&M)
- [2026-06-25] Mark/Matthew to confirm TC8 / year-end roll-forward with DP. (owner: Mark/Matthew) (source: Granola - M&M)
- [2026-06-25] Add XBRL to the Slack chat / roadmap. (owner: Mark) (source: Granola - M&M)

- [2026-07-01] Feed real production data through the native GL engine in dev to validate it (expected to surface code/architecture changes). (owner: Mark) (source: Linear status update)
- [2026-07-01] Decide the FX balance rule (single-currency spike vs native multi-currency) and confirm the full residual account list. (owner: Design/DP) (source: Slack #accounting-mvp)
- [2026-07-01] Define the VAT correction/control account in the chart of accounts (separate from the normal VAT account; empty after each quarterly suppletie). (owner: Mark/DP) (source: Slack #accounting-mvp)
- [2026-07-01] Design the locked-period audit log + Slack unlock alerting (report all changes first, add amount thresholds later). (owner: Mark) (source: Slack #accounting-mvp)

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project (this project is In Progress, so they are posted as a proposed comment, not auto-applied)._
- (project: Start writing to neno's double-entry GL) Insert-only ledger with reversals — no edits to journal entries; corrections reverse and rebook. (source: Granola — Next Steps AGL, 22 Jun 2026)
- (project: Start writing to neno's double-entry GL) Period closes define immutability; closed periods lock writes by default; unlocking is approval-gated, insert-only, and fully audited. (source: Granola — DP session, 23 Jun 2026)
- (project: Start writing to neno's double-entry GL) VAT: corrections after close booked in the next period (<EUR 1,000 folds in); balance sheet carries three VAT lines (receivable, payable, corrections/suspense); breakdown by rate/territory; export to Nextens. (source: Granola — DP session, 23 Jun 2026)
- (project: Start writing to neno's double-entry GL) Multi-currency: store foreign amount + transaction-date rate, derive euro on demand; month-end revaluation of FX assets/liabilities to an unrealized FX gains/losses account. (source: Granola — DP session, 23 Jun 2026)
_Expanded 2026-06-26 from the native-GL knowledgebase (PR #1128). This project is In Progress, so these are posted as a proposed comment, not auto-applied._
- (project: Start writing to neno's double-entry GL) Every posting balances - committed iff debits equal credits; money is integer minor units with sign = direction; balances follow the normal-balance convention. (source: PR #1128 INV-LEDGER-01/03)
- (project: Start writing to neno's double-entry GL) Booking is atomic and reliable: one event -> one balanced entry committed in a single transaction, retried until booked, never silently dropped, idempotent under retry. (source: PR #1128 INV-LEDGER-05/06)
- (project: Start writing to neno's double-entry GL) Provider-independent ledger: Neno owns its chart of accounts and VAT codes (seeded once from Exact, Neno-owned thereafter); any external sync is a removable downstream mapping; posting never lazily creates accounts. (source: PR #1128 INV-LEDGER-04/07)
- (project: Start writing to neno's double-entry GL) Explicit, addressable lineage: each entry references its event and source document; each contra references its original; reverse-at-most-once; liveness derived from the reference graph; per-leg undo (unaccepting a payment reverses only the settlement, the bill stays recognised). (source: PR #1128 INV-LEDGER-08/09)
- (project: Start writing to neno's double-entry GL) Counterparty and VAT code are line dimensions; AP/AR are single accounts drilled down by counterparty (no account-per-party); human-readable descriptions are rendered from structure, not stored. (source: PR #1128 INV-LEDGER-10/11)
- (project: Start writing to neno's double-entry GL) Each entry carries a posting timestamp and an audit timestamp; the financial period is derived from the posting timestamp in the owner's timezone. (source: PR #1128 INV-LEDGER-12)
- (project: Start writing to neno's double-entry GL) Cash completeness: every bank transaction is booked on import (bank vs suspense); reconciliation/allocation reclassifies the amount out of suspense, so suspense holds exactly the unreconciled tail. (source: PR #1128 INV-LEDGER-13)
- (project: Start writing to neno's double-entry GL) VAT-aware postings: each event type books a fixed balanced set; VAT treatment (domestic single leg vs self-assessed two legs for reverse-charge/intra-EU/import) drives the shape; the VAT return is computed from code-tagged lines and mapped to boxes. (source: PR #1128 INV-LEDGER-06)
- (project: Start writing to neno's double-entry GL) [deferred] Period locking with approval + full audit (break-the-glass); a source-document change propagates as corrective bookings and is refused in a locked period without break-the-glass. (source: PR #1128 INV-LEDGER-14/15)
- (project: Start writing to neno's double-entry GL) [deferred] Multi-currency: store native amount + transaction-date rate, derive reporting currency on demand; period-end FX revaluation of foreign assets/liabilities to an unrealised FX gain/loss. (source: PR #1128 INV-LEDGER-16)
- (project: Start writing to neno's double-entry GL) [deferred] Opening-balance import so balance-sheet accounts are absolute totals (balance-sheet source of truth); related-party drill-down by counterparty. (source: PR #1128 INV-LEDGER-17/18)
- (project: Start writing to neno's double-entry GL) [deferred] VAT corrections after close: under EUR 1,000 folds into the next period; over threshold filed as a supplemental return posted day 1 to a distinct VAT corrections account (the third balance-sheet VAT line). (source: PR #1128 INV-LEDGER-19)
- (project: Start writing to neno's double-entry GL) [deferred] Full statutory report set from Neno's own data (trial balance, GL export, P&L, balance sheet, AR aging 30/60/90/120+, fixed-asset register, per-account drill-down); real-time bank balance; XBRL filing of the VAT return as registered consulent; year-end roll-forward into retained earnings. (source: PR #1128 INV-LEDGER-20/21/22, TC-LEDGER-15)

_Expanded 2026-06-30 from the DP/Mark open-questions session (posted as a proposed comment; project is In Progress)._
- (project: Start writing to neno's double-entry GL) FX rate: book at the ECB daily reference (mid) rate on the transaction date, frozen on the line; a settlement rate difference posts to a dedicated realised FX gain/loss account, and a separate bank FX fee to bank charges. (source: Granola DP/Mark, 30 Jun / Slack #accounting-mvp, 1 Jul)
- (project: Start writing to neno's double-entry GL) Every line stores native amount + transaction-date rate; the reporting-currency value is derived, never stored alone; balance = signed sum of reporting-currency values (INV-LEDGER-23/27/01). (source: Slack #accounting-mvp, 1 Jul)
- (project: Start writing to neno's double-entry GL) [deferred] Period-end FX revaluation of balance-sheet accounts only to the period-end rate, true-up to the FX result account, USD bank first, on demand (INV-LEDGER-16). (source: Slack #accounting-mvp, 1 Jul)
- (project: Start writing to neno's double-entry GL) [deferred] Locked-period break-the-glass: correct-forward by default; closed-period restatement only via a deliberate, approver-gated, fully audited unlock with amount-threshold alerting (INV-LEDGER-14/15). (source: Granola DP/Mark, 30 Jun)
- (project: Start writing to neno's double-entry GL) VAT is always corrected forward; two VAT balance-sheet accounts (normal + corrections/control); once the EUR 1,000 cumulative threshold is crossed all subsequent corrections route to the corrections account until the suppletie is filed (INV-LEDGER-19). (source: Slack #accounting-mvp, 1 Jul)

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-23] Agentic-ledger idea: when a backdated entry is posted, automatically detect which reports are affected and surface the delta. (source: Granola — DP session)
- [2026-06-26] Full spec for this build lives in the native-GL knowledgebase (an Obsidian vault) on PR #1128: user-observable outcomes in 'General Ledger - Truth Conditions' (TC-LEDGER-01..15), system rules in 'General Ledger - Invariants' (INV-LEDGER-01..22), and the architecture narrative in the 'General Ledger' domain hub. In-scope-now items (TC-01..06 / INV-01..13) are marked 'Holds'; deferred future-build items (TC-07..15 / INV-14..22) are marked 'Proposed (deferred)'. (source: PR #1128 knowledgebase)
- [2026-06-26] The knowledgebase is a behavioural 'digital twin' built as a one-way chain: Truth Condition -> Invariant -> Scenario -> test -> code, traceable by id (TC-/INV-/SCN-LEDGER-NN); tests cite the scenario id they prove and code cites the invariant id it satisfies. (source: PR #1128 knowledgebase README)
