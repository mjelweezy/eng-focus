# Running context — Source of truth for all bookkeeping data
_Initiative: 0f26a21f-cd9b-47e4-9678-a3c5107a1fa0 · maintained by the daily job + Matthew_
_Last updated: 2026-08-27

> Split out of `source-of-truth.md` (initiative ce07f00e) on 30 Jul 2026. Covers the external
> data integrations feeding neno's books: Numbrs, Stripe, Shopify, Shopify Payments, WeFact,
> PEPPOL, generic platform balance imports. See `source-of-truth-activity.md` for the
> accountant-performed bookkeeping actions on top of this data. Full pre-split history lives in
> the archived `source-of-truth.md`.

## Decisions
- [2026-06-25] (carried forward) Three of the next-5 cohort run payroll that currently needs a manual monthly CSV import from Numbrs; payroll-integration viability for Q3 to be determined. (source: Granola/Slack - M&M week)
- [2026-08-10] Payroll (Nmbrs) design settled in a PRD interview with Matthew and written into the Linear project: entries trigger on payroll-run completion with no approval step; one balanced entry per client per payroll period; both the neno GL and the client's Exact administration are written by neno, with Nmbrs' native Exact export switched off per client; neno owns the wage-code -> neno chart -> client Exact chart mapping per client; net wage payment clearing is in scope; connection and cutover are per client; postings appear in booking history with line-level drill-down and no dedicated payroll screen in v1; monthly and 4-weekly (13-period) payroll are both supported. Success = payroll in the neno GL matches Exact to the cent, the native push is disabled for every in-scope client, and accountants can reconcile wage payment clearing. Rollout proves on Cohort 2. (source: Linear project description, Payroll (Numbrs integration), 10 Aug)
- [2026-08-10] Payroll journals are on the Nmbrs REST API (api.nmbrsapp.com, shipped Mar 2026); only webhook management is SOAP and that is one-time per-debtor UI config, so the 1 Mar 2027 SOAP retirement does not affect this project. (source: Linear project description, Payroll (Numbrs integration), 10 Aug)
- [2026-08-10] The WeFact/neno invoicing question is scoped to invoicing completeness only - whether neno customers can send invoices on par with WeFact, even by a different process - not to broader platform gaps. Analysis starts from Cohort 2, where only 3 customers actively use invoicing, and is done by manual review rather than scraping. (source: Granola - kick off wefact/neno invoicing, 10 Aug)

- [2026-08-14] The adopted Exact-to-neno transition-date guidance names WeFact and NMBRS alongside Swan and Open Banking as tools to be cut off from Exact and enabled on neno on a customer's transition date - so the payroll and invoicing cutovers are now bound to the same per-customer date rather than being sequenced independently. (source: Slack #tech-team (Yaroslav), 14 Aug)

- [2026-08-18] WeFact ingestion landed as two pieces, both on the untracked "Neno Services Onboarding" project: a scheduled pull of WeFact documents so payables reach the review queue (NEO-1922, Yaroslav, Done 18 Aug) and a per-workspace transition date deciding which transactions neno reconciles and exports (NEO-1897, Done 18 Aug). Importing WeFact sales invoices and credit notes as read-only neno invoices through a single shaping function is in progress (NEO-1950). (source: Linear NEO-1897/1922/1950, 18 Aug)
- [2026-08-19] The WeFact connector is treated as the significant unblocker for this initiative: accountants can process AR and AP from WeFact data without the customer first migrating to neno invoicing. It only became possible after the CI/CD egress fix gave the API a stable Cloud NAT IP for the IP whitelisting WeFact requires (NEO-1949). (source: Granola - Daily stand up, 19 Aug; Linear NEO-1949)
- [2026-08-19] Nothing moved on Numbrs payroll requirements in the window - the two open Nmbrs tickets are build work, a per-workspace Nmbrs connection with a live token (NEO-1807) and listing a connected client's payroll runs (NEO-1808), both In Progress. Stripe, Shopify and PEPPOL were not discussed in any meeting in the window. (source: Linear NEO-1807/1808; Granola, 6-20 Aug)

- [2026-08-27] WeFact connector unblocked (CI/CD egress / Cloud NAT fix), landed 19 Aug - a significant accelerant for AR/AP, since accountants can process both without the customer migrating to neno invoicing first; relevant to the 'later' WeFact Invoicing item on this initiative. (source: Granola - WeFact/Credit Notes sessions, 19 Aug 2026)

## Open questions
- [open] (carried forward) Payroll design not yet discussed — open design area for a future session. (project: Payroll (Numbrs integration))
- [open] (carried forward) When will a direct neno invoicing API be available? A reseller-style prospect's decision to use the WeFact bridge now or wait depends on the roadmap timeline. (owner: Matthew) (source: Granola - Bjorn - Neno Invoicing connect, 28 Jul)
- [open] Payroll entry granularity - company total, cost centre or employee level - to settle with the accountants. (project: Payroll (Numbrs integration)) (source: Linear project description, 10 Aug)
- [open] Payroll open decisions: TWK corrections into closed or filed periods; the failure mode when the Exact leg fails; whether entries need a source document (leaning no); whether neno's chart already carries the payroll accounts. (project: Payroll (Numbrs integration)) (source: Linear project description, 10 Aug)
- [open] Is Nmbrs' native Exact export in fact running per client? The 15 Jun Escontrela review found memoriaal entry 26900001 created by an accountant, which reads as hand-entry; settled from the entry's creator field by anyone with Exact access, and the per-client cutover depends on the answer. (project: Payroll (Numbrs integration)) (source: Linear project description, 10 Aug)
- [open] Which reminder functionality and send methods do cohort customers actually use in WeFact? (source: Granola - kick off wefact/neno invoicing, 10 Aug)

- [open] Does the per-client Nmbrs cutover have to happen on the customer's Exact transition date, or can payroll cut over separately? The 14 Aug onboarding guidance implies the former; the payroll PRD assumes per-client cutover on its own schedule. (owner: Adam/Yaroslav) (source: Slack #tech-team, 14 Aug; Linear project description, 10 Aug)

- [2026-08-27] No Granola/Slack activity found in the last 14 days on Stripe, Shopify, Shopify Payments, PEPPOL or generic platform balance imports - all remain undiscussed 'later' items. (source: run review, 2026-08-27)

## Risks
_None carried forward yet — see source-of-truth.md for pre-split risk history._
- [med] (2026-08-10) Invoicing feature gaps against WeFact: at least one cohort client invoices in USD and neno has no multi-currency invoicing, and there is no pay-online link on invoices. A payment link is wanted before the end of August but the engineers are stretched. (source: Granola - kick off wefact/neno invoicing, 10 Aug)
- [low] (2026-08-10) Rollout beyond the payroll pilot cannot be sized until the client payroll inventory requested from the accountants on 3 Aug comes back. (source: Linear project description, Payroll (Numbrs integration), 10 Aug)

- [med] (2026-08-19) The WeFact work that unblocks this initiative sits entirely on "Neno Services Onboarding", a project attached to no initiative, so the board's own "later" items (PEPPOL, Neno invoicing improvements, Stripe, Shopify, Shopify Payments, WeFact Invoicing) show no movement while the real integration work runs outside the initiative. (source: Linear, 18-19 Aug)

## Next steps
- [2026-07-15] (carried forward) Matthew to grab CSV examples from Numbrs customers to understand the payroll reconciliation shape. (owner: Matthew) (source: Granola/tldv - stand-up, 15 Jul)
- [2026-07-28] (carried forward) Send Bjorn (Smart Data Solutions) a proposal covering how the WeFact invoicing route would work now and when direct neno API integration is expected, so he can decide whether to proceed or wait. (owner: Matthew) (source: Granola - Bjorn - Neno Invoicing connect, 28 Jul)
- [2026-08-10] Share the next 10 Cohort 3 customers to narrow the invoicing gap analysis, and send Frederique the known invoicing feature-gap list. (owner: Matthew) (source: Granola - kick off wefact/neno invoicing, 10 Aug)
- [2026-08-10] Frederique to complete Swan sandbox ID verification to unlock full neno feature access, and run a comparison of the neno monorepo/Linear against WeFact's public pages to catch commercially promoted features neno may be missing. (owner: Frederique) (source: Granola - kick off wefact/neno invoicing, 10 Aug)

## Projects (filed in Linear)
- [2026-07-30] Attached to this new initiative: Payroll (Numbrs integration), Third-party wallet transaction import (MVP). New backlog items from the Q3 roadmap deck not yet filed as Linear projects: Shopify, Shopify Payments, WeFact Invoicing, PEPPOL invoicing, Generic platform balance imports.

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Third-party wallet transaction import (MVP)) Needed so non-Swan banking customers can feed transactions into neno (bypassing the Swan requirement); start with Stripe, then additional channels. (source: DP session / Q3 planning, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Not covered in the 23 Jun DP session; requirements still to be defined. (source: DP session, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Payroll postings must reach the neno ledger, not only Exact - investigate CSV-based ingestion from Numbrs (8 customers, ~12 payroll payments/month); selective push of payroll transactions to Exact for hybrid customers. (source: Granola/tldv - stand-ups, 15 Jul)
- (project: Payroll (Numbrs integration)) One balanced entry per client per payroll period, triggered on payroll-run completion with no human approval step: wage costs, employer social security, holiday allowance and 13th month debit; net wages payable, payroll tax payable and provisions credit. VAT-irrelevant, balanced to the cent, not fragmented. (source: Linear project description, 10 Aug 2026)
- (project: Payroll (Numbrs integration)) neno writes both ledgers - its own GL and the client's Exact administration - and the native Nmbrs Exact export is switched off per client. Nmbrs stays the payroll engine. (source: Linear project description, 10 Aug 2026)
- (project: Payroll (Numbrs integration)) neno owns and maintains the per-client mapping from Nmbrs wage codes/accounts to the neno chart to the client's Exact chart, visible in neno; client charts genuinely differ (4000/1670 standard, 40000/17000 legacy, 1680 variants) and the Nmbrs GL schema is not exportable. (source: Linear project description, 10 Aug 2026)
- (project: Payroll (Numbrs integration)) Net wage payment clearing is in scope: salary payments must be reconcilable against the payable the entry creates, including advances, remainders and split payments. (source: Linear project description, 10 Aug 2026)
- (project: Payroll (Numbrs integration)) Payroll postings appear in booking history alongside other postings, drillable to line level; no dedicated payroll screen in v1. Both monthly and 4-weekly (13-period) payroll must record correctly. (source: Linear project description, 10 Aug 2026)
- (project: Payroll (Numbrs integration)) Out of scope: running payroll in neno, HR/employee data, initiating salary payments, other payroll providers, EOR/foreign payroll, wage tax declarations and pension exports. (source: Linear project description, 10 Aug 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
