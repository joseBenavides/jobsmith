# Why the sweep rules exist

Every rule in the `source` skill is there because a sweep can fail in a way that looks exactly like success. That is the whole problem: a bad sweep and a good sweep produce the same shape of report, and the user cannot tell them apart. These are the failure modes, so you can recognise them before they cost someone a role.

Read this before deciding any sweep rule is optional.

## The eight ways a sweep quietly lies

**1. It judges a source by its summary.**
A job-alert digest names one role in its subject line and carries five more inside. The preview text is generated from the first listing, so a six-role email is indistinguishable from a one-role email until you open it. Skim the subjects and you lose most of what arrived, while your report still says you processed the inbox. There is no heuristic that makes this safe, and no budget argument either: opening a message is cheap, and a missed role is not recoverable once the posting closes.

**2. It converts its own blind spots into verdicts.**
An agent that cannot open a page has learned something about its own reach, not about the job. If that becomes "role not found", the user never hears about a live posting. Keep the two apart: the site answered and the role is gone, versus you could not get an answer. Only the first is a finding. The second gets flagged and handed over with its link.

**3. It trusts a search box to filter.**
Job-site search is often loose or semantic, and some employer APIs return the whole board regardless of the query. Read the first twenty rows of that and you have an unfiltered dump wearing the costume of a filtered result: a query for design leadership comes back led by a marketing coordinator and an accountant. Pull the fuller list and filter the titles yourself.

The corollary matters just as much. When a search tool returns nothing, that can mean the tool cannot express the query, not that the market is empty. Reporting the second when the first is true tells the user their field has dried up when it has not.

**4. It reports a channel it never ran.**
Skipping a channel and saying it "added nothing" is worse than skipping it openly, because it tells the user a place has been looked. They stop wondering about it. That is why every channel carries one of three verdicts, and why "swept" requires having actually queried it. Verifying a role that another channel already surfaced is verification work, not sourcing.

**5. It starts from today after missing a week.**
Fixed lookback windows cannot survive an outage longer than the window. Miss four days with a four-day window and everything in the gap is gone permanently: the postings expire, and nothing in the system ever knew they existed. Derive the lookback from the actual gap since the last run, and work the oldest items first, because those are closest to expiring.

This also means the agent has to record its own runs. Scheduled jobs get skipped far more often than people assume, and without a trail there is no way to notice.

**6. It kills a company on one angry sentence.**
Search results surface the sharpest lines in a review base, which biases every culture judgment toward the kill. A single review is not a pattern, a three-year-old cluster is not a description of the company today, and problems inside a department the user would never join are a caveat rather than a disqualifier. Culture filtering with a low standard of proof removes good employers silently, and the user never learns what was taken off the table.

When the read is genuinely uncertain, that is a real answer and it belongs in front of the user, with the quotes and the review count. Uncertainty surfaced is useful. Uncertainty resolved into a silent kill is not.

**7. It writes a row it never read back.**
A create call returning success means the request was accepted, not that the row is complete or useful. A row missing its link cannot be acted on, so it may as well not exist, and nobody notices until the user goes looking. Read the rows back and check the fields. This generalises past rows: re-open the page you edited, re-read the file you changed. Tool success is not an artifact.

**8. It lets one track starve.**
When someone searches two tracks, the one with louder job titles and a longer alias list attracts more queries, and the quieter one comes back thin. That reads like an empty market when it is really an unqueried one. Count queries per track and keep them level.

## The pattern underneath all eight

Every one of these is the same mistake: **treating an inference as an observation.** A subject line inferred to be the whole email. A failed fetch inferred to be a dead role. A search result inferred to be a filtered result. A success response inferred to be a completed write.

The fix is the same each time, and it is the cheapest habit in this repo: **go read the actual thing.** Open the message, poll the employer's own board, pull the full list, query the row back. When you genuinely cannot, say so with a link, and let the user decide.

## What the user should be able to check

A sweep report should let someone verify quality without redoing the work:

- **Every row has a working link.** The fastest possible check, and it catches sloppy writes immediately.
- **Every "nothing found" carries a number.** "Their careers page answered with 34 open roles, none matching" is a finding. "Nothing found" alone might mean the source was never reached.
- **Every channel has a verdict**, and skipped means skipped.
- **Anything unresolved is listed with its link**, rather than absent.

If a report is missing those, the honest read is that the sweep was thinner than it looks.
