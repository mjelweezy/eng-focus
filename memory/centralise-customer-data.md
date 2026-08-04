# Running context — Centralise customer data
_Initiative: e78d13c9-27d8-494e-9c3b-8a264412e471 · maintained by the daily job + Matthew_
_Last updated: 2026-08-04_

> New initiative created 30 Jul 2026 from the Q3 roadmap deck's "Centralise the data" goal: one
> system for every customer's data. Covers basic reporting, structured profiles for services
> customers, and onboarding actions for off-platform tasks.

## Decisions
- [2026-07-30] (Matthew) Initiative created; scoped to the 3 named features only (Basic reporting, Structured profiles for services customers, Onboarding actions for off-platform tasks) rather than the deck's broader "Accountant/Onboarding Efficiency" and "Integrate sales source" buckets.
- [2026-07-30] Standard P&L layout is the baseline for all customers, with five top-level components: Revenue, Gross Profit, Net Profit, Total Operating Expenses (collapsible) and Cash Balance (as of the last accounting close). (source: Granola - Reporting, 30 Jul)
- [2026-07-30] Accountant approval gates customer access: the report is hidden until an accountant approves it for the first time; later approvals update the "Last reviewed" timestamp. (source: Granola - Reporting, 30 Jul)
- [2026-07-30] The approved report is stored as a JSON snapshot in neno's own database; the customer view renders that snapshot rather than making a live Exact call. (source: Granola - Reporting, 30 Jul)
- [2026-07-30] Reporting lives under a new top-level tab, not under Money Management - it is accounting/bookkeeping reporting, not money management. (source: Granola - Reporting, 30 Jul)
- [2026-08-03] PDF export: the monthly breakdown renders landscape, everything else portrait; the cover page shows the "Approved on" date rather than "Generated". (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] Presentation rules: green for positive and red for negative; negatives shown with a minus sign instead of brackets; report language follows the customer's platform language. (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] A customer hitting the report error screen triggers a Slack notification to the team. (source: Granola - Review reporting, 3 Aug)

## Open questions
- [open] Which data points do customers want glanceable on the home page? Ask DP before sharing the current design, to avoid premature sign-off. (owner: Matthew) (source: Granola - Review reporting, 3 Aug)
- [open] Exact PDF phrasing for the approved-on date ("Last updated" vs "Approved on"), and how the reviewed-by line should read - to confirm with DP. (owner: Eugenia) (source: Granola - Review reporting, 3 Aug)
- [open] Period-filter date range: read the available range out of the stored JSON if possible; if not, cap the "to" period at the last approved month. (project: Custom reporting for Neno customers) (source: Granola - Review reporting, 3 Aug)
- [open] Where the new reporting tab sits in the right-hand menu - Eugenia to explore. (owner: Eugenia) (source: Granola - Review reporting, 3 Aug)
- [open] Which additional report templates are needed beyond "most" and hospitality. (owner: Dmytro/DP) (source: Granola - Review reporting, 3 Aug)

## Risks

## Next steps
- [2026-08-03] Ask DP which home-page data points customers want, before sharing the current design. (owner: Matthew) (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] Show the customer-facing view (not the accountant view) to Tonique at the next review. (owner: Matthew/Dmytro/Eugenia) (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] Eugenia to explore the new menu-tab placement for reporting and confirm the PDF "last updated" phrasing with DP. (owner: Eugenia) (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] (done) Matthew to generate Linear tickets from the 3 Aug transcript and share with Dmytro and Eugenia - NEO-1652 to NEO-1670 filed on the Custom reporting project the same day.

## Projects (filed in Linear)
- [2026-07-30] Attached existing project "Custom reporting for Neno customers" (basic reporting). "Structured profiles for services customers" and "Onboarding actions for off-platform tasks" have no Linear project yet - listed as text items on the board only.
- [2026-08-03] Twelve issues filed on "Custom reporting for Neno customers" out of the 3 Aug review (NEO-1652 through NEO-1670), covering the customer-facing report, the approval / "books are clean" flow, storing Exact data on approval, hourly refresh, email send, period-picker limits, the compare button, layout and PDF changes, and Slack error alerting. NEO-1624 (port the report generator into the Swan banking admin) and NEO-1648 (translations into all eight banking-app languages) are Done.

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Custom reporting for Neno customers) Standard P&L layout as the baseline for all customers: Revenue, Gross Profit, Net Profit, collapsible Total Operating Expenses, and Cash Balance as of the last accounting close. (source: Granola - Reporting, 30 Jul 2026)
- (project: Custom reporting for Neno customers) Store the approved report JSON in neno's own database on approval; the customer view renders the stored snapshot, never a live Exact call. (source: Granola - Reporting, 30 Jul 2026)
- (project: Custom reporting for Neno customers) The report is hidden from the customer until an accountant approves it for the first time; later approvals update the "Last reviewed" timestamp. (source: Granola - Reporting, 30 Jul 2026)
- (project: Custom reporting for Neno customers) Customers see "Last reviewed by [accountant] on [date/time]" after approval - a rolling indicator of the last reconciled state, not a live accuracy guarantee. (source: Granola - Reporting, 30 Jul 2026)
- (project: Custom reporting for Neno customers) The customer view strips accountant-specific fields (Exact connection info, company selector, accountant-side indicators) but keeps filters and period selection. (source: Granola - Reporting, 30 Jul 2026)
- (project: Custom reporting for Neno customers) Reporting lives under a new top-level tab, not under Money Management. (source: Granola - Reporting, 30 Jul 2026)
- (project: Custom reporting for Neno customers) The approval button requires a confirmation dialog reading "By clicking confirm, the customer will be informed this data is up to date". (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) Accountants must be able to assign a report template per customer, and Eugenia needs visibility of all templates in order to style them. (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) Month-over-month compare button plus an optional monthly column breakdown (Jan-Dec plus YTD). (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) Enabling the report per customer is done from the accounting engagement screen, with an assigned accountant. (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) On first approval, explore emailing the customer "Your management report is ready". (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) PDF export: monthly breakdown landscape, otherwise portrait; cover page shows the "Approved on" date, not "Generated". (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) Presentation: green positive / red negative, negatives with a minus sign rather than brackets, and report language following the customer's platform language. (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) A customer hitting the report error screen triggers a Slack notification to the team. (source: Granola - Review reporting, 3 Aug 2026)
- (project: Custom reporting for Neno customers) Drive the period filter from the range actually available per workspace, read out of the stored JSON; today the picker accepts any month and year, including periods that do not exist for that workspace. (source: Granola - Review reporting, 3 Aug 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
