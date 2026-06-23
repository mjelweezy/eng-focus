# Running context (memory layer)

One markdown log per initiative. This is **persistent memory** — it accumulates over time and is NOT wiped by the daily run.

## How it's used
- The 6am job **reads** each initiative's log and folds durable items (decisions, open questions, risks, next steps, notes) into the rendered `context.json` — so the page remembers things older than the 14-day source lookback.
- The job also **appends** newly-discovered durable items it finds in Linear/Granola/Slack back into the log (deduped), and marks open questions resolved when it sees them answered.
- The page (`context.html`) is unchanged in structure — it's just informed by this memory.

## How Matthew adds context
Either edit these files directly, or just tell Claude in chat ("file this against the GL initiative: …"). Chat-fed items are recorded here tagged `(Matthew)` and **surfaced on the page** by default. Say "keep internal" to record without surfacing (mark the bullet `(internal)`).

## Format conventions (keep these so the job can parse reliably)
- Dated bullets: `- [YYYY-MM-DD] <text> (source: …)`
- Open questions: prefix `[open]` or `[resolved YYYY-MM-DD]`.
- Risks: prefix `[high]` / `[med]` / `[low]`.
- Anything tagged `(internal)` informs Claude's summary but is not shown on the page.
- Manual / chat-fed entries are authoritative — the job never edits or removes them.

## Files
- `onboarding-5-customers.md` → initiative cb65425b
- `double-entry-gl.md` → initiative fef38f90
- `source-of-truth.md` → initiative ce07f00e
