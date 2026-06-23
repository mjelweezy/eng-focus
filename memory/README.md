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

## Write-back to Linear (daily)
The morning job publishes requirements from memory back into Linear project descriptions, with a comment trail.

- **Source of truth:** memory is canonical; the Linear project description is a published view. The job never treats its own writes as new input.
- **Managed region only:** the job edits ONLY the block between these markers, leaving all other (human-authored) text untouched:
  ```
  <!-- BEGIN auto-maintained requirements · edit memory, not here -->
  ## Requirements (auto-maintained · updated YYYY-MM-DD)
  - <requirement> (source: …)
  <!-- END auto-maintained -->
  ```
  If a project has no markers yet, the job APPENDS a fresh managed block (it does not delete existing description text).
- **Backlog / Planned / Todo projects:** the managed block is written into the description.
- **In Progress / In Review projects:** description is NOT edited; new requirements are posted as a comment only (labelled "proposed").
- **Completed / Cancelled:** skipped.
- **Change history:** on any change, the job posts a project comment (save_comment with projectId) summarising the diff (+ added / ~ updated / − removed) with the date and source. No change → no write and no comment (idempotent).
- **Attribution:** requirement bullets in memory can be tagged `(project: <name>)`. Untagged items the job is confident about are auto-filed; ambiguous ones go under `## Unfiled requirements (needs attribution)` in the initiative's memory and are reported, for Matthew to assign (in chat or by editing the tag). Nothing ambiguous is written to a project.

### Memory section a project requirement should live in
Use `## Requirements by project` with sub-bullets tagged to a project, e.g.:
```
## Requirements by project
- (project: Financial reporting) Aged receivables in 30/60/90/120+ buckets. (source: DP session, 23 Jun)
```
