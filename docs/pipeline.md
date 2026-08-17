# The pipeline: data model and tracker conventions

One row per opportunity. This model is identical in both tracker modes (Notion database or `my/pipeline.csv`); the mode only changes where the rows live and how the user edits them.

## Statuses

`Sourced -> Approved -> Tailored -> Applied -> Interviewing -> Offer -> Closed`

| Status | Meaning | Who sets it |
|---|---|---|
| Sourced | Found and worth the user's look | Agent |
| Approved | User said "yes, pursue this" | **User only.** Approval is always the user's click; nothing proceeds without it |
| Tailored | Application kit drafted and ready for review | Agent, when the kit is done |
| Applied | User actually sent it | User (or agent on the user's say-so) |
| Interviewing | Any interview scheduled or in progress | Either |
| Offer | Offer received | User |
| Closed | Over, for any reason, good or bad | Either |

## The closed discipline

A bare `Closed` teaches nothing. Every closed row carries **Closed Reason** and **Closed On**:

`hired` (the good one) · `passed` (user chose not to pursue) · `rejected-at-screen` · `rejected-after-interview` · `position-filled` · `position-pulled` · `ghosted` (no response after 30+ days) · `withdrew` · `declined-offer` · `stale` (aged out at Sourced)

Reasons are data. Three `rejected-at-screen` in a row on one track is a resume problem; three `rejected-after-interview` is prep material; heavy `passed` means sourcing quality is off. The weekly review module reads these patterns; capture them honestly.

## Columns (canonical, both modes)

| Column | Type | Notes |
|---|---|---|
| Role | title/text | "Role Title" |
| Company | text | |
| Track | select | The user's track names from `my/profile.md` |
| Status | select | See above |
| Fit Score | number 1-5 | Agent's honest read against the profile |
| Fit Notes | text | Why that score, one or two lines |
| Link | URL | The posting |
| Location | text | Include work mode: "NYC (hybrid)", "Remote US" |
| Comp Posted | text | Only what the posting states publicly |
| Contact | text | Names/roles known at this company; details live in the kit log |
| Next Action | text | The one next thing: "send thank-you", "follow up w/ recruiter" |
| Next Action Date | date | When it is due. This column powers the returning brief |
| Date Sourced | date | |
| Date Applied | date | |
| Closed Reason | select | Required when Status = Closed |
| Closed On | date | Required when Status = Closed |
| Notes | text | Anything else |

Dates are `YYYY-MM-DD` in both modes.

## Direct manipulation and reconcile

The user edits the tracker directly (toggling a Notion select, editing the CSV in any spreadsheet app). They never have to tell the agent about a change. At every session start the agent:

1. Reads the tracker.
2. Notes what changed since it last looked (new Approved rows are work orders; new Closed rows need reasons if missing).
3. Surfaces due or overdue Next Actions in the returning brief.

If a Closed row is missing its reason, ask once, casually, and record it. Never nag.

## Notion mode

Created automatically during onboarding when a Notion connector is present. Build:

- A database named "Job Pipeline" with the columns above (Status, Track, and Closed Reason as selects with the exact option lists).
- Views, if the connector supports creating them: **Board by Status** (the main surface) · **Active** (table, Status is not Closed) · **Action due** (table, Next Action Date is not empty, sorted ascending) · **Closed** (table, for the record).
- Store the database ID in `my/state.json` so future sessions find it without searching.

## CSV mode

`my/pipeline.csv`, header row exactly matching the Columns table order. The user edits it in Excel, Google Sheets, Numbers, or a text editor. Rules the agent follows: never reorder or rename headers; append rows at the bottom; treat the file as the single source of truth even if it looks hand-mangled, and repair gently rather than overwrite.

## The dashboard (CSV mode's table-with-filters)

After any pipeline change, regenerate `my/pipeline.html` from the template at `assets/pipeline-dashboard.html`: copy the template and replace the `/*JOBSMITH_ROWS*/[]` placeholder with the rows as a JSON array (keys: `role, company, track, status, fit, location, next_action, next_action_date, date_applied, link, closed_reason`). The result is a single self-contained file: status counts, search, status and track filters, sortable columns, overdue next-actions highlighted. Read-only by design; edits happen in the CSV. Notion users don't need it (their views are better) but can ask for it.
