# Running context — Make neno the source of truth for all bookkeeping
_Initiative: ce07f00e · maintained by the daily job + Matthew_

## Decisions
- [2026-06-23] Aged-receivables analysis (by customer, 30/60/90/120+ day buckets) is a minimum AR reporting requirement. (source: Granola — Double-Entry Bookkeeping Open Questions)
- [2026-06-19] End-to-end AR reconciliation is now a tracked Linear project (lead David, Planned) — first concrete piece of this initiative.

## Open questions
- [open] Payroll design not yet discussed — open design area for a future session.
- [open] Full reporting requirements list still being compiled by DP.
- [open] Feature sequencing and ownership for the post-GL bookkeeping scope not yet decided. (owner: Matthew)

## Risks
- [med] Scope is broad and unsequenced; nothing staffed yet beyond AR reconciliation (David).
- [med] Full reporting requirements not yet enumerated — scope could grow once DP's list lands.

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
- (project: Depreciation & accruals) Material accruals discovered post-close (e.g. legal claims, missed intercompany interest) are handled via approval-gated, insert-only adjustment entries with a full audit log. (source: DP session, 23 Jun 2026)
- (project: Related-parties register) Supports intercompany bookings; intercompany interest auto-accrual was deprioritised as a nice-to-have. (source: DP session, 23 Jun 2026)
- (project: Payroll (Numbrs integration)) Not covered in the 23 Jun DP session; requirements still to be defined. (source: DP session, 23 Jun 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-23] (Source: DP design session, 23 Jun 2026) Aged-receivables reporting (30/60/90/120+ buckets by customer) is a minimum requirement → captured on the Financial reporting project. Depreciation/accruals and intercompany interest-accrual notes captured on their respective projects; payroll not yet discussed.
