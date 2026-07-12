# Running context — Build data by onboarding 5 additional customers
_Initiative: cb65425b · maintained by the daily job + Matthew_
_Last updated: 2026-07-12_

## Decisions
- [2026-06-22] Onboarding is a simple hardcoded checklist — a backend boolean/timestamp per step that hides when complete. (source: Granola)
- [2026-06-22] Onboarding fixed to 6 steps (connect Swan, connect external bank, view transactions, reconcile/respond to tasks, send first invoice, contact accountant); team invites, accounting menu, WhatsApp and credit-card steps deferred. (source: Granola)
- [2026-06-22] Onboarding completion is self-reported per task (boolean/timestamp per user row adjacent to the workspace); auto-detection of completed steps deliberately avoided to keep it simple. (source: Granola — Matthew/Eugenia weekly sync)
- [2026-06-22] Both the transactions drawer and the tasks/upload drawer should expose all three bill-submission options (WhatsApp, email forwarding, Vault); email forwarding must be feature-flagged to selected customers and the customer's forwarding address must show in the Vault UI. (source: Granola — weekly sync)
- [2026-06-16] Open-banking-only users get a limited Home (no team invites, card creation, transfers, or manage-beneficiaries — all tied to a Swan bank account), and the Home is hidden after onboarding for now. (source: Granola — User Journey for next 5 customers)
- Non-Swan customers must be able to connect to neno (bypassing the Swan requirement) — a prerequisite for the next 5. (source: Granola)
- Slack notifications required for all document uploads during the early phase. (source: Slack #accounting-mvp)
- [2026-06-23] Open-banking provider selected: Montoya; first end-to-end test to run in preview using a personal account once prod keys land. (source: Granola)
- [2026-06-23] First open-banking target customer is As Controla (no Swan account, so non-Swan access must work). (source: Granola)
- [2026-06-23] Onboarding calls targeted for 6-7 July; Joel executing the onboarding-five build next week while Matthew is away. (source: Granola)
- [2026-06-24] Onboarding dashboard redesign (Giuseppe) shipped to production. New policy: vibe-coded work must ship in small, reviewable batches, or be frontend-only — no backend/DB changes until engineering assesses feasibility. (source: Granola — Daily stand-up)
- [2026-06-24] Exact OAuth tokens are per-connection, not per-division; chosen approach for now is one token reused across workspaces with the division stored per connection (connection pool / backpressure deferred to the roadmap). (source: Granola — Daily stand-up)
- [2026-06-24] Exact export automation works as a local script; to be codified into the accounting service for nightly syncs once accountants sign off. (source: Granola — Daily stand-up)
- [2026-06-24] Multi-Client Exact: per-workspace Exact writes + GL/VAT reads (M2) shipped; follow-up to separate OAuth grants from workspace division assignments is in progress. (source: Linear NEO-1329 / NEO-1348)
- [2026-06-25] Onboarding uses magic-link sign-on: customers create a workspace, log in, and self-onboard; reuse existing pages and link out rather than build custom components. (source: Granola - Onboarding Actions with Dima / Three amigos, 25 Jun)
- [2026-06-25] Onboarding tasks are self-marked; hard-code one task per workspace with a hyperlink back to the onboarding homepage. Completed tasks are hidden (not deleted); once all are done the homepage is hidden and removed from nav. The invoice task is optional (not required to trigger hiding). (source: Granola - 25 Jun)
- [2026-06-25] The Transactions tab is hidden until a bank account is connected; open-banking connect is a single button from Neno that hands off to the provider-controlled flow. (source: Granola - 25 Jun)
- [2026-06-25] Accountant chat exists but is not yet available and is not surfaced in onboarding for now; the Bills & expenses page is removed from consideration for this cohort. (source: Granola - 25 Jun)
- [2026-06-25] The 5 new customers mostly do not yet use the Neno app and will need open banking; Matthew onboards them by phone next week, so the platform must be ready before he returns. Dima and Eugenia (Enya) own building out the onboarding steps. (source: Granola - Onboarding Actions with Dima, 25 Jun)
- [2026-06-25] Onboarding homepage visual design: a lighter layout (moving away from chunky cards), the active/next task highlighted in purple, white card backgrounds; the accountant profile block is copied onto the tasks screen so it stays visible after the homepage is hidden. (source: Granola - Three amigos: onboarding actions, 25 Jun)
- [2026-06-25] Page visibility for open-banking customers: show the Account, Transactions and Invoices pages; the Transactions page appears once a bank is connected and transactions exist in the table; the Bills & expenses page is .build-only and out of scope for .co. (source: Granola - Onboarding Actions with Dima, 25 Jun)
- [2026-06-25] Onboarding actions use separate checklist items (not a modal); the example task links out to the tasks page rather than a custom inline view; Joel's first version (built alongside dynamic tasks) needs rework. (source: Granola - Onboarding Actions with Dima, 25 Jun)
- [2026-06-25] Bank-connect uses the Yapily ('Yapi') model - one button from Neno hands off to the provider-controlled flow; the homepage shows connected accounts and prompts for additional ones; WhatsApp setup collapses once connected. (source: Granola - Three amigos, 25 Jun)
- [2026-06-25] Dummy onboarding task detail: task types are 'clarification' or 're-upload receipt'; it surfaces the WhatsApp + email-forwarding sharing methods (as in transactions) and is discoverable from both the notification bell and the transactions view. (source: Granola - Three amigos, 25 Jun)
- [2026-06-26] (Matthew) The 'Whatsapp, Email forwarding and Vault re-provisioning' project (d5958e60d05c) was renamed to 'Feature re-provisioning for non Swan customers' and broadened to making all relevant platform aspects work for non-Swan customers; a TC4 (Money Management) was added. (source: Linear project)

- [2026-07-01] Open Banking is now being tested against a real bank: Yaroslav connected his ABN AMRO account and hit the bankTransaction.reference VARCHAR(255) limit immediately - Open Banking reference strings can run far longer (the spec sets no firm cap; providers observed 500-280,000 chars), so a schema change is needed before ingestion is reliable (Yaroslav to align on schema with Mark before opening the PR). (source: Slack #tech-team, 1 Jul)
- [2026-07-02] Multi-Client Exact Online Connections shipped and marked Completed: Ops manage per-workspace Exact connections from the admin Exact Connections page; each workspace reads/writes its own Exact division (Ocean Ionics is no longer the hard-coded fallback); OAuth grants are separated from workspace/division assignments; broken connections are detected, shown in the Ops dashboard and alerted to #tech-critical; the accountant UI fails closed when Exact is missing/unhealthy. Merged PRs #1102/#1107/#1116/#1131/#1133. (source: Linear project status update, 2 Jul)

- [2026-07-07] (Matthew) 'Enable team members outside Swan' descoped for July: the first five customers will be single users only, with manual user-add as a quick fix. Replaced on the board by 'Enable invoicing for non-Swan customers'; priority is IBAN selection for open banking customers.

- [2026-07-06] LOE automation direction: automate the Letter of Engagement (one button, pre-filled per entity, signing tracked back into HubSpot); PandaDocs ruled out on cost and Google Workspace has no signature API - likely DocuSign or an EU open-source signing tool. HubSpot deal context (group structure, pain points, sales history) to be surfaced in the neno accounting-engagement screen, avoiding paid HubSpot seats for accountants. (source: Granola - Matthew/Eugenia weekly sync, 6 Jul)
- [2026-07-07] Open banking is now testable; Dima is plugging Yapily into the onboarding actions. The customer transaction view is HIDDEN initially (data can be messy) - show account name and balance only; consent captured in the DB allows re-pulling transactions later. (source: Granola - 3 amigos: Walk through customer onboarding, 7 Jul)
- [2026-07-07] Non-Swan workspaces: contract signing auto-creates a fresh empty workspace (no Swan link). Cashback onboarding: a new screen prompts card order during onboarding for Swan users; the cashback prompt was removed from the account page; the upsell idea (show open-banking-only users projected 1% cashback if they open a Swan account) is parked. (source: Granola - 3 amigos / weekly sync, 6-7 Jul)

- [2026-07-08] Open banking production and preview API keys are live in both environments; Joel is testing open banking with Revolut and the new auth flows - ready to merge when tests pass. (source: Granola - Daily stand-up, 8 Jul)
- [2026-07-08] Onboarding sequencing: Joel to finalise onboarding actions with Dima, then move to single order line; the fake/dummy onboarding task is picked up after the open-banking items. New engineers arrive 3 Aug, so scoped lanes of work must be ready before then. (source: Granola - Daily stand-up, 8 Jul)
- [2026-07-08] The contact recipe component (email/WhatsApp + QR code) for the Task page is blocked on Dima's unpublished component (built for Transactions); the goal is to reuse it rather than rebuild. (source: Granola - Matthew/Euge, 8 Jul)
- [2026-07-10] Onboarding Actions implementation has started in Linear: the accountant directory + assign-accountant-on-workspace-creation shipped (NEO-1468, Done 10 Jul) and the Home onboarding hub screens from Euge's design are In Progress (NEO-1467) - the first issues filed on the project. (source: Linear)
- [2026-07-10] Bills uploaded via dynamic-task file_upload responses now enter the OCR/ingestion pipeline (NEO-1462 fixed, Joel, 10 Jul) - previously they were stored only as Vault documents and never became reviewable Bills (TC3 contradiction closed). (source: Linear NEO-1462)

## Open questions
- [open] Onboarding stepper is a placeholder until the new transactions UI is ready. (owner: Euge)
- [resolved 2026-06-24] Open-banking provider decision → provider selected: Montoya (contract still unsigned as of 23 Jun; Plaid ~EUR 2k/mo minimum was the prior front-runner).
- [resolved 2026-06-24] Montoya open-banking contract — now received (24 Jun); prod-key gating requirements being scoped this week. (source: Granola — Daily stand-up)
- [resolved 2026-07-01] Open-banking prod-key gating requirements being scoped this week. (owner: Joel) -> resolved: Open Banking is now being tested end-to-end against a real ABN AMRO account in preview (Slack #tech-team, 1 Jul).
- [open] How does Exact count rate limits — per token or per division? Determines whether a connection pool actually helps. (source: Granola — Daily stand-up, 24 Jun)
- [open] Onboarding V2 deprecation date conflict: Swan email says 26 Jun, live docs say 30 Sep - Cecile to confirm. (source: Granola)
- [open] Receipt upload drawer is missing WhatsApp + email options (flagged 22 Jun).
- [open] When will the new transactions UI (by-date/by-status switch + open-tasks section) be ready? The full WhatsApp/email/Vault submission walkthrough depends on it. (source: Granola — weekly sync)
- [open] Accountant assignment for new workspaces: add to Yaroslav's accounting-engagements page, or hard-code for the initial five? (source: Granola - Onboarding Actions, 25 Jun)
- [open] The dummy onboarding task must be visually marked as a dummy, and all three receipt-sharing methods (WhatsApp, email forwarding, Vault) must be explored before it can be marked done. (source: Granola - 25 Jun)

## Risks
- [high] 6 Jul onboarding target is tight — onboarding-actions project still in backlog and its stepper depends on the new transactions UI.
- [med] Email forwarding only accepts workspace-member senders, has no UI yet, rejected-email auto-reply still to build.
- [descoped 2026-06-26] (Matthew) Swan card-limit + direct-debit fixes (public onboarding link, Onboarding V2 migration) are a separate banking workstream and are NOT relevant to this onboarding initiative - removed from risks.
- [med] Montoya open-banking contract received 24 Jun; prod keys still gate the open-banking end-to-end test (requirements being scoped). (source: Granola — Daily stand-up)
- [low] (Matthew, 2026-06-26) We now have what we need to get Open Banking live for review on Monday 29 Jun; prod keys remain the only gate for the full end-to-end test.
- [resolved 2026-07-02] Exact OAuth rework: a new table to store access/refresh tokens per connection is required before Exact write functionality is fully usable. -> shipped: Multi-Client Exact completed 2 Jul, OAuth grants separated from workspace/division assignments and per-workspace writes live. (source: Linear project status update)
- [med] Exact API rate limit (60 req/min) already hit in testing with seeded data; needs a roadmap solution (connection pool or backpressure). (source: Granola — Daily stand-up, 24 Jun)
- [med] Open-banking transaction ingestion needs a schema change: bankTransaction.reference (VARCHAR(255)) truncates/errors on real ABN AMRO data; OB references can reach ~280k chars. Schema/perf trade-off (large TEXT + substring lookups) to be agreed with Mark first. (source: Slack #tech-team, 1 Jul)
- [med] WhatsApp/Meta Business account setup is misconfigured and was deprioritised (24 Jun); blocks the WhatsApp bill channel rollout. (source: Granola — Daily stand-up)

## Next steps
- Design the user-journey screens + an Ocean Ionics-specific homepage. (owner: Euge)
- WhatsApp messaging update + email reply automation. (owner: Ihor)
- Check Swan drawer configurability; leave Linear tickets for Joel. (owner: Dima)
- All team members test WhatsApp + email forwarding before Ocean Ionics rollout. (owner: Team)
- Flag the missing email/WhatsApp options in the drawer to Joel (explanation required if intentionally absent). (owner: Team)
- [2026-06-23] Finalise acceptance criteria + non-Swan user journey before Matthew is away. (owner: Matthew, by EOW) (source: Granola)
- [2026-06-23] Fix the public onboarding link + pass email to the Swan API. (owner: Nick/Matthew, by Fri 26 Jun) (source: Granola)
- [2026-06-24] Test the full open-banking flow once Montoya prod keys arrive. (owner: Engineering, 24 Jun) (source: Granola)
- [2026-06-24] Introduce a new table for Exact access/refresh tokens per connection; complete the OAuth rework. (owner: Ihor) (source: Granola — Daily stand-up)
- [2026-06-24] Scope out the open-banking prod-key requirements this week. (owner: Joel) (source: Granola — Daily stand-up)
- [2026-06-24] Resolve the WhatsApp/Meta Business account issue with Giuseppe (low priority, can slip to next week). (owner: Joel) (source: Granola — Daily stand-up)
- [2026-06-24] Codify the Exact export automation into the accounting service once accountants sign off. (owner: Ihor) (source: Granola — Daily stand-up)
- [2026-06-25] Matthew to write up the onboarding requirements before going on leave. (owner: Matthew) (source: Granola)
- [2026-06-25] Dima & Euge own building out the onboarding steps together, agreeing a decision-making framework to resolve open questions independently next week. (owner: Dima/Euge) (source: Granola)
- [2026-06-25] Euge to iterate on the onboarding prototype and the open-banking integration. (owner: Euge) (source: Granola)
- [2026-06-25] Ihor & Joel to fix the Transactions page visibility/permissions for open-banking customers. (owner: Ihor/Joel) (source: Granola)
- [2026-06-25] Test the magic-link onboarding flow end-to-end in a new workspace. (owner: Dima/Euge) (source: Granola - Onboarding Actions with Dima)

- [2026-07-07] Euge: document the customer-onboarding user journey as-is (HubSpot screenshots as placeholders); share the updated task-screen prototype + missing-context summary in Slack for Dima. (source: Granola, 6-7 Jul)
- [2026-07-07] Matthew: review onboarding screens for open-banking customers (incl. the cashback prompt); prioritise Q3 bookkeeping features for the first five. (source: Granola, 6-7 Jul)
- [2026-07-07] Yaroslav: prototype a HubSpot agent in the existing chat interface; book time with Euge to walk the user journey. (source: Granola - 3 amigos, 7 Jul)

- [2026-07-08] Matthew to check with Dima on availability of the unpublished contact component for the Task page. (owner: Matthew) (source: Granola - Matthew/Euge, 8 Jul)
- [2026-07-08] Euge while Matthew is away: start the customer-journey work (entity grouping on the Account Engagement page + main customer pain points) and record/share the drawer-to-overlay UI migration video for async review. (owner: Euge) (source: Granola - Matthew/Euge, 8 Jul)

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Whatsapp, Email forwarding and Vault re-provisioning) The transactions drawer and the tasks/upload drawer must both offer all three bill-submission channels: WhatsApp, email forwarding, and Vault upload. (source: Granola — User Journey, 16 Jun 2026)
- (project: Whatsapp, Email forwarding and Vault re-provisioning) Email forwarding must be feature-flagged so it only shows for selected customers, and the customer's email-forwarding address must be displayed in the Vault UI. (source: Granola — weekly sync, 22 Jun 2026)
- (project: Present onboarding actions for the next five customers) Home dashboard presents a 6-step, self-reported onboarding checklist (connect Swan, connect external bank, view transactions, reconcile/respond to tasks, send first invoice, contact accountant); steps are self-marked, with no auto-detection. (source: Granola — weekly sync, 22 Jun 2026)
- (project: Present onboarding actions for the next five customers) Open-banking-only users get a limited Home (no team invites, card creation, transfers, or manage-beneficiaries), and the Home is hidden after onboarding for now. (source: Granola — User Journey, 16 Jun 2026)
- (project: Feature re-provisioning for non Swan customers) [TC4 Money Management] A non-Swan account holder sees the Transactions page populated with history for all bank accounts connected via open banking (empty table if none connected); the Accounts and Invoicing pages are also visible and functional. (source: Linear project TC4, added by Matthew 26 Jun 2026)

- (project: Enable customers to connect external bank accounts and view their transactions) Bank-transaction reference storage must accommodate Open Banking reference strings far beyond 255 characters (the OB spec sets no firm cap; providers observed up to ~280,000 chars) - the current VARCHAR(255) truncates/errors on real ABN AMRO data. (source: Slack #tech-team, 1 Jul)

- (project: Enable customers to connect external bank accounts and view their transactions) The customer-facing transaction view is hidden initially for open-banking accounts (data can be messy) - show account name and balance only; capture consent in the DB so transactions can be re-pulled/backfilled later. (source: Granola - 3 amigos walkthrough, 7 Jul 2026)
_Note (2026-07-08): requirements tagged 'Present onboarding actions for the next five customers' publish to the successor project 'Onboarding Actions for the Next Five Customers' (1f7bfeff). Not appended there this run: both bullets are already reflected verbatim in that project's hand-authored outline (TC1/limited-Home/hide-when-done)._

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-22] (internal) LLM-assisted changes risk being left half-done — watch for partial reworks during the onboarding push. (source: Granola — weekly sync)
