# Running context — Source of truth for all bookkeeping data
_Initiative: 0f26a21f-cd9b-47e4-9678-a3c5107a1fa0 · maintained by the daily job + Matthew_
_Last updated: 2026-07-30_

> Split out of `source-of-truth.md` (initiative ce07f00e) on 30 Jul 2026. Covers the external
> data integrations feeding neno's books: Numbrs, Stripe, Shopify, Shopify Payments, WeFact,
> PEPPOL, generic platform balance imports. See `source-of-truth-activity.md` for the
> accountant-performed bookkeeping actions on top of this data. Full pre-split history lives in
> the archived `source-of-truth.md`.

## Decisions
- [2026-06-25] (carried forward) Three of the next-5 cohort run payroll that currently needs a manual monthly CSV import from Numbrs; payroll-integration viability for Q3 to be determined. (source: Granola/Slack - M&M week)

## Open questions
- [open] (carried forward) Payroll design not yet discussed — open design area for a future session. (project: Payroll (Numbrs integration))
- [open] (carried forward) When will a direct neno invoicing API be available? A reseller-style prospect's decision to use the WeFact bridge now or wait depends on the roadmap timeline. (owner: Matthew) (source: Granola - Bjorn - Neno Invoicing connect, 28 Jul)

## Risks
_None carried forward yet — see source-of-truth.md for pre-split risk history._

## Next steps
- [2026-07-15] (carried forward) Matthew to grab CSV examples from Numbrs customers to understand the payroll reconciliation shape. (owner: Matthew) (source: Granola/tldv - stand-up, 15 Jul)
- [2026-07-28] (carried forward) Send Bjorn (Smart Data Solutions) a proposal covering how the WeFact invoicing route would work now and when direct neno API integration is expected, so he can decide whether to proceed or wait. (owner: Matthew) (source: Granola - Bjorn - Neno Invoicing connect, 28 Jul)

## Projects (filed in Linear)
- [2026-07-30] Attached to this new initiative: Payroll (Numbrs integration), Third-party wallet transaction import (MVP). New backlog items from the Q3 roadmap deck not yet filed as Linear projects: Shopify, Shopify Payments, WeFact Invoicing, PEPPOL invoicing, Generic platform balance imports.

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Third-party wallet transaction import (MVP)) Needed so non-Swan banking customers can feed transactions into neno (bypassing the Swan requirement); start with Stripe, then additional channels. (source: DP session / Q3 planning, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Not covered in the 23 Jun DP session; requirements still to be defined. (source: DP session, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Payroll postings must reach the neno ledger, not only Exact - investigate CSV-based ingestion from Numbrs (8 customers, ~12 payroll payments/month); selective push of payroll transactions to Exact for hybrid customers. (source: Granola/tldv - stand-ups, 15 Jul)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
