# Running context — Centralise customer data
_Initiative: e78d13c9-27d8-494e-9c3b-8a264412e471 · maintained by the daily job + Matthew_
_Last updated: 2026-08-28

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
- [2026-08-04] An approval publishes the whole history under a single date and is insert-only - the period pickers are navigation and never scope what is published. The stored snapshot holds one whole-year ledger per fiscal year in the render layer's serialized shape, plus cash and bank movement per period, and carries a version so an unrecognised payload is reported unreadable rather than mis-rendered. The Exact division is its own column, not just a field inside the payload. (source: Linear project description, Custom reporting for Neno customers, 4 Aug)
- [2026-08-04] The approver is not persisted: attribution reads "Approved by [accountant] on [date]", resolved from Workspace.assignedAccountantId at read time and degrading to "Approved by accountant on [date]" when none is assigned. This supersedes the earlier "Last reviewed by" wording. (source: Linear project description, Custom reporting for Neno customers, 4 Aug)
- [2026-08-11] The approved management report is now shown to every customer (NEO-1789), rendered by a single audience-agnostic display-and-export component that both admin and the customer app use (NEO-1679) - so the accountant and the customer see the same report surface. (source: Linear NEO-1789 / NEO-1679, 10-11 Aug)
- [2026-08-12] Custom reporting gets a demo mode in Atlas: pick a business type and a company name and render a sample report for prospects (NEO-1797). (source: Linear NEO-1797, 12 Aug)

- [2026-08-13] Accounting features (Tasks, Bill Forwarding, Open Banking, WhatsApp) are gated on a real accounting engagement rather than on the customer having a Swan account (NEO-1830), the Vault is treated as a feature of every workspace with only its email forwarding an accounting feature (NEO-1848), and the accountant card is unified across Home and Tasks (NEO-1847) - all Dima, all shipped 13 Aug. (source: Linear NEO-1830/1847/1848, 13 Aug)
- [2026-08-14] Management report presentation work is in review: an indigo pie palette and denser PDF typography (NEO-1895, Dima), following the 13 Aug refresh of the restaurant dummy data (NEO-1839). (source: Linear NEO-1839, 13 Aug; NEO-1895, 14 Aug)
- [2026-08-14] An "Accountant Portfolio Dashboard" (NEO-1840) is now queued to Dima as planned work - the first movement on the accountant-portfolio question that has sat open since Yaroslav proposed Atlas as its home. (source: Linear NEO-1840, 14 Aug)

- [2026-08-18] The reporting header is not settled: Nick is still unhappy with the "Powered by Neno" treatment, so Eugenia is to timebox two hours on variants and escalate for more time if all of them are rejected. (source: Granola - Bills & Expenses walk through, 18 Aug)
- [2026-08-18] Onboarding actions must be re-pointed from "Vault" to "Bills & Expenses" when Bills & Expenses ships, and the forwarding-email banner moves with them. (source: Granola - Bills & Expenses walk through, 18 Aug)
- [2026-08-19] The accountant portfolio dashboard shipped as the admin home page (NEO-1911, Dima, Done 19 Aug) - but on the untracked "Unified Review Queue" project rather than under this initiative. A platform metrics page was added alongside it; it is considered useful beyond accountants (mirrorable on a TV screen and inside Atlas) and needs a wording polish pass. (source: Linear NEO-1911, 19 Aug; Granola - Matthew / Euge, 19 Aug)
- [2026-08-19] Accounting-engagement screen direction agreed from Art's proposal: drop per-workspace accountant assignment so all workspaces sit under one accountant, put a copy icon inline next to the bill-forwarding email address, and render the signs-in-with field as a link when it is a magic link rather than a dropdown. (source: Granola - Matthew / Euge, 19 Aug)

- [2026-08-27] Reporting stays in EUR for all customers, with FX conversion applied at the ledger level, not per report. (project: Custom reporting for Neno customers) (source: Granola - Reporting/Platform sync, week of 24 Aug 2026)
- [2026-08-27] Accountant homepage: a platform metrics page was added to the accountant dashboard (mirrors on TV/Atlas); the accountant tasks page was agreed to be redesigned onto the user-facing task screen design, with a Linear ticket to be filed under Bookkeeping Improvements and assigned to Dima; quick filters for accountants agreed (filter by client with open task count, dropdown not chips, first card open by default); glass effect confirmed accountant-only screens should diverge from customer UI and not get the glass treatment. (source: Granola - Platform/accountant UI sessions, week of 24 Aug 2026)
- [2026-08-28] Reporting scope is under commercial pressure from e-commerce prospects: three deals raised in #tech-team (~EUR 45k combined ACV) want inventory visibility inside financial reporting, live inventory valuation, COGS tracking down to the purchase batch and gross-margin analysis, and a fourth wants Neno reporting data pulled into his own dashboard over MCP. Matthew's read, not yet a decision: neno is more likely to integrate with best-in-class e-commerce tooling that already solves inventory - as POS tooling like Tebi does for horeca - than to build inventory management itself, and this needs discovery. (source: Slack #tech-team, 28 Aug 2026)

## Open questions
- [open] Which data points do customers want glanceable on the home page? Ask DP before sharing the current design, to avoid premature sign-off. (owner: Matthew) (source: Granola - Review reporting, 3 Aug)
- [open] Exact PDF phrasing for the approved-on date ("Last updated" vs "Approved on"), and how the reviewed-by line should read - to confirm with DP. (owner: Eugenia) (source: Granola - Review reporting, 3 Aug)
- [open] Period-filter date range: read the available range out of the stored JSON if possible; if not, cap the "to" period at the last approved month. (project: Custom reporting for Neno customers) (source: Granola - Review reporting, 3 Aug)
- [open] Where the new reporting tab sits in the right-hand menu - Eugenia to explore. (owner: Eugenia) (source: Granola - Review reporting, 3 Aug)
- [open] Which additional report templates are needed beyond "most" and hospitality. (owner: Dmytro/DP) (source: Granola - Review reporting, 3 Aug)
- [open] Which workspace does an approval publish to? The admin page selects an Exact division and roughly 118 divisions have no neno workspace at all; resolving through WorkspaceExactConnection and refusing to approve an unattached division is the proposed route. (project: Custom reporting for Neno customers) (source: Linear project description + NEO-1651, 4 Aug)
- [open] Should approving a still-open month be allowed - approving on the 4th publishes a month holding four days of bookings - or should the accountant be able to view but not publish it? (project: Custom reporting for Neno customers) (source: Linear project description, 4 Aug)
- [open] Inside a covered range, should a month with no bookings render as zero (what Exact's absent rows produce today) or as a visible "no data" marker? (project: Custom reporting for Neno customers) (source: Linear project description, 4 Aug)

- [open] Structured profiles for services customers: WeFact has a customer overview screen with multiple contacts per organisation, while neno has only a name field, no contacts and no customer overview screen. What is the data model, and does it come before or after the HubSpot-backed profile view Frederique owns? (owner: Frederique/Matthew) (source: Granola - Freddy <> Matthew, 12 Aug)

- [2026-08-27] Reporting header treatment ('Powered by Neno') still not signed off by Nick; Euge timeboxed to 2 hours on variants - if all are rejected this needs escalation. (project: Custom reporting for Neno customers) (source: Granola, week of 24 Aug 2026)
- [open] How much of the inventory-management and inventory-reporting space should neno slice off itself versus integrate with existing e-commerce tooling? Needs discovery before Q4, when e-commerce becomes a focus vertical. (owner: Matthew) (source: Slack #tech-team, 28 Aug 2026)

## Risks

- [2026-08-27] Euge to present reporting header variants to Nick within the 2-hour timebox. (owner: Eugenia) (source: Granola, week of 24 Aug 2026)
- [2026-08-27] Euge to file a Linear ticket for the accountant tasks page redesign, assigned to Dima under Bookkeeping Improvements; update task card designs before Dima picks them up. (owner: Eugenia) (source: Granola, week of 24 Aug 2026)
- [2026-08-27] Schedule the open banking onboarding standardization meeting (Matthew, Euge, Yaroslav) to define when new customers connect via Lendroom vs. neno's own open banking - not yet held as of 27 Aug. (owner: Eugenia) (source: Granola - Bills & Expenses walkthrough, 18 Aug 2026)

## Next steps
- [2026-08-03] Ask DP which home-page data points customers want, before sharing the current design. (owner: Matthew) (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] Show the customer-facing view (not the accountant view) to Tonique at the next review. (owner: Matthew/Dmytro/Eugenia) (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] Eugenia to explore the new menu-tab placement for reporting and confirm the PDF "last updated" phrasing with DP. (owner: Eugenia) (source: Granola - Review reporting, 3 Aug)
- [2026-08-03] (done) Matthew to generate Linear tickets from the 3 Aug transcript and share with Dmytro and Eugenia - NEO-1652 to NEO-1670 filed on the Custom reporting project the same day.
- [2026-08-05] Email Marloes (Ocean Ionics) once the balance sheet, P&L and cost-centre dashboard is live on her neno account - expected the week of 10 Aug - so she can assess whether it is useful. (owner: Matthew) (source: Granola - Ocean Ionics Monthly Neno catch up, 5 Aug)
- [2026-08-06] Match the report PDF output to Eugenia's design and add end-to-end tests; Andries can start approving management reports in production from end of day 6 Aug. (owner: Dmytro) (source: Slack #tldv-channel - daily stand-up, 6 Aug)
- [2026-08-07] Custom reporting functionality is complete and the UI shipped to production; remaining work is the per-customer report layout, hourly Exact refresh, email send, the compare button and the error-screen Slack alert. (owner: Dmytro) (source: Granola - Daily stand up, 7 Aug)

- [2026-08-18] Timebox two hours on reporting-header variants for Nick, and escalate if all are rejected. (owner: Eugenia) (source: Granola - Bills & Expenses walk through, 18 Aug)
- [2026-08-19] File the accountant tasks-page redesign ticket against Bookkeeping Improvements and assign it to Dmytro. (owner: Matthew) (source: Granola - Matthew / Euge, 19 Aug)
- [2026-08-19] Share the accounting-engagement screen design with Art for feedback. (owner: Eugenia) (source: Granola - Matthew / Euge, 19 Aug)
- [2026-08-28] Matthew to meet Max next week on the API/MCP roadmap and the e-commerce reporting asks (inventory, COGS, margin). (owner: Matthew) (source: Slack #tech-team, 28 Aug 2026)

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
- (project: Custom reporting for Neno customers) An approval publishes the entire history under one date and is insert-only; rows are never updated or deleted, and approving again inserts a new row alongside the existing ones. (source: Linear project description, 4 Aug 2026)
- (project: Custom reporting for Neno customers) The stored snapshot holds one whole-year ledger per fiscal year in the render layer's serialized shape, plus cash and bank movement per period, and carries a version; an unrecognised version is reported as unreadable rather than mis-rendered. (source: Linear project description, 4 Aug 2026)
- (project: Custom reporting for Neno customers) The Exact division is stored as its own column on the approval row, so reassigning a workspace's division can never serve the customer another company's approved figures. (source: Linear project description, 4 Aug 2026)
- (project: Custom reporting for Neno customers) Attribution reads "Approved by [accountant] on [date]", resolved from Workspace.assignedAccountantId at read time and degrading to "Approved by accountant on [date]" when none is assigned - the date is never dropped. This supersedes the earlier "Last reviewed by" wording. (source: Linear project description, 4 Aug 2026)
- (project: Custom reporting for Neno customers) A window read out of a snapshot takes the requested months in order, sums them for the period total, takes the comparative from the same months of the previous year in the same snapshot, and treats the cash balance as cumulative point-in-time - never summed across windows. (source: Linear project description, 4 Aug 2026)

_Expanded 2026-08-20 from Linear (18 Aug). Custom reporting for Neno customers is Backlog, so this publishes into its managed description block._
- (project: Custom reporting for Neno customers) Demo mode must accept a CSV import so the sample report is built from the prospect's own figures rather than generic sample data. (source: Linear NEO-1953, 18 Aug 2026)
- (project: Custom reporting for Neno customers) Reporting is presented in EUR for all customers, with FX conversion applied at the ledger level rather than per report. (source: Granola - Reporting/platform sync, week of 24 Aug 2026)

## Unfiled requirements (needs attribution)
_New requirements the job couldn't confidently assign to a project land here for Matthew to file._

- [2026-08-19] Structured customer profiles for services customers - a customer overview screen with multiple contacts per organisation, matching what WeFact offers - is a board text item under this initiative with no Linear project, and it overlaps Frederique's HubSpot-backed profile view; needs Matthew's attribution. (source: Granola - Freddy <> Matthew, 12 Aug; Granola - Matthew / Euge, 19 Aug)

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
