# Running context — Build data by onboarding 5 additional customers
_Initiative: cb65425b · maintained by the daily job + Matthew_

## Decisions
- [2026-06-22] Onboarding is a simple hardcoded checklist — a backend boolean/timestamp per step that hides when complete. (source: Granola)
- [2026-06-22] Onboarding fixed to 6 steps (connect Swan, connect external bank, view transactions, reconcile/respond to tasks, send first invoice, contact accountant); team invites, accounting menu, WhatsApp and credit-card steps deferred. (source: Granola)
- Non-Swan customers must be able to connect to neno (bypassing the Swan requirement) — a prerequisite for the next 5. (source: Granola)
- Slack notifications required for all document uploads during the early phase. (source: Slack #accounting-mvp)

## Open questions
- [open] Onboarding stepper is a placeholder until the new transactions UI is ready. (owner: Euge)
- [open] Open-banking provider decision still unconfirmed (Plaid ~EUR 2k/mo minimum); single- vs multi-provider pending.
- [open] Receipt upload drawer is missing WhatsApp + email options (flagged 22 Jun).

## Risks
- [high] 6 Jul onboarding target is tight — onboarding-actions project still in backlog and its stepper depends on the new transactions UI.
- [med] Open-banking provider decision unconfirmed.
- [med] Email forwarding only accepts workspace-member senders, has no UI yet, rejected-email auto-reply still to build.

## Next steps
- Design the user-journey screens + an Ocean Ionics-specific homepage. (owner: Euge)
- WhatsApp messaging update + email reply automation. (owner: Ihor)
- Check Swan drawer configurability; leave Linear tickets for Joel. (owner: Dima)
- All team members test WhatsApp + email forwarding before Ocean Ionics rollout. (owner: Team)

## Notes / manual context
<!-- Matthew's chat-fed context lands here, tagged (Matthew). Surfaced on the page by default. -->
