# Running context — Build data by onboarding 5 additional customers
_Initiative: cb65425b · maintained by the daily job + Matthew_
_Last updated: 2026-06-24_

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

## Open questions
- [open] Onboarding stepper is a placeholder until the new transactions UI is ready. (owner: Euge)
- [resolved 2026-06-24] Open-banking provider decision → provider selected: Montoya (contract still unsigned as of 23 Jun; Plaid ~EUR 2k/mo minimum was the prior front-runner).
- [open] Montoya open-banking contract still unsigned as of 23 Jun; prod keys expected 24 Jun, then full flow tested in preview. (source: Granola)
- [open] Onboarding V2 deprecation date conflict: Swan email says 26 Jun, live docs say 30 Sep - Cecile to confirm. (source: Granola)
- [open] Receipt upload drawer is missing WhatsApp + email options (flagged 22 Jun).
- [open] When will the new transactions UI (by-date/by-status switch + open-tasks section) be ready? The full WhatsApp/email/Vault submission walkthrough depends on it. (source: Granola — weekly sync)

## Risks
- [high] 6 Jul onboarding target is tight — onboarding-actions project still in backlog and its stepper depends on the new transactions UI.
- [med] Email forwarding only accepts workspace-member senders, has no UI yet, rejected-email auto-reply still to build.
- [med] Swan blockers for higher card limits + direct debit: public onboarding link must be fixed and migration to Onboarding V2 completed; Nick & Matthew targeting fixes by Fri 26 Jun. (source: Granola)
- [med] Montoya open-banking contract unsigned as of 23 Jun - signature + prod keys gate the open-banking test. (source: Granola)

## Next steps
- Design the user-journey screens + an Ocean Ionics-specific homepage. (owner: Euge)
- WhatsApp messaging update + email reply automation. (owner: Ihor)
- Check Swan drawer configurability; leave Linear tickets for Joel. (owner: Dima)
- All team members test WhatsApp + email forwarding before Ocean Ionics rollout. (owner: Team)
- Flag the missing email/WhatsApp options in the drawer to Joel (explanation required if intentionally absent). (owner: Team)
- [2026-06-23] Finalise acceptance criteria + non-Swan user journey before Matthew is away. (owner: Matthew, by EOW) (source: Granola)
- [2026-06-23] Fix the public onboarding link + pass email to the Swan API. (owner: Nick/Matthew, by Fri 26 Jun) (source: Granola)
- [2026-06-24] Test the full open-banking flow once Montoya prod keys arrive. (owner: Engineering, 24 Jun) (source: Granola)

## Requirements by project
_Tagged requirements the daily job publishes into each Linear project's auto-maintained block._
- (project: Whatsapp, Email forwarding and Vault re-provisioning) The transactions drawer and the tasks/upload drawer must both offer all three bill-submission channels: WhatsApp, email forwarding, and Vault upload. (source: Granola — User Journey, 16 Jun 2026)
- (project: Whatsapp, Email forwarding and Vault re-provisioning) Email forwarding must be feature-flagged so it only shows for selected customers, and the customer's email-forwarding address must be displayed in the Vault UI. (source: Granola — weekly sync, 22 Jun 2026)
- (project: Present onboarding actions for the next five customers) Home dashboard presents a 6-step, self-reported onboarding checklist (connect Swan, connect external bank, view transactions, reconcile/respond to tasks, send first invoice, contact accountant); steps are self-marked, with no auto-detection. (source: Granola — weekly sync, 22 Jun 2026)
- (project: Present onboarding actions for the next five customers) Open-banking-only users get a limited Home (no team invites, card creation, transfers, or manage-beneficiaries), and the Home is hidden after onboarding for now. (source: Granola — User Journey, 16 Jun 2026)

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
- [2026-06-22] (internal) LLM-assisted changes risk being left half-done — watch for partial reworks during the onboarding push. (source: Granola — weekly sync)
