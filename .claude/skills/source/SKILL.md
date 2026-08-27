---
name: source
description: Sweep the user's channels for roles worth their time, score them honestly, and write new Sourced rows to the pipeline. Run when the user asks to source, sweep, or find roles, when they ask what is out there, or on a recurring schedule they set up. Also evaluates a single posting they hand you.
---

# Source

Find roles the user would actually want, and put them in front of them without wasting their attention. A sweep that returns twenty mediocre rows is worse than one that returns two good ones, because the user pays for every row in review time.

Read `AGENT.md` first. Hard rules apply, especially: never guess a URL, never apply to anything, read the whole source rather than a summary, missing data never kills, and verify before you claim.

`docs/sweep-quality.md` explains the failure modes behind the rules below. Read it if a call is close, and before you decide any of this is optional.

## Definition of done

A sweep is not finished until you can show these six things. Put them in the report; a check whose evidence is missing did not happen.

| # | Check | Evidence to show |
|---|---|---|
| 1 | **Gap check and backfill** , how long since the last sweep, and the lookback widened to cover it | "Last sweep 12 days ago, backfilling; looked back 15 days" |
| 2 | **Every source read in full** , no judging a listing or a digest from its subject or snippet | sources processed, roles found |
| 3 | **Every channel has a verdict** , SWEPT, SKIPPED, or BLOCKED | the channel ledger |
| 4 | **Every channel reported empty carries a count** | "careers page answered, 34 open roles, 0 matches" |
| 5 | **Rows read back after writing** , every required field present | "3 rows written, 3 pass the field check" |
| 6 | **Nothing unresolved was dropped** , unverifiable roles written with a flag, uncertain culture surfaced, both with links | the "needs your eyes" section |

## Inputs

- `my/profile.md` , tracks, locations, work modes, authorization, constraints, dealbreakers.
- `my/channels.md` , the researched channel plan per track, from onboarding. **This is also the sweep's memory**: see "Keep the channel plan alive" below.
- The tracker , to dedupe against what is already there.

**Missing channel plan?** Say so and offer to run the channel research step from onboarding first; a sweep without it is guesswork. If they would rather sweep now, use general search against their profile and mark the results as unresearched-channel finds.

## Step 0: Check the gap, then backfill

Before sweeping, work out how long it has been since the last one (`my/state.json` records it). **Missed sweeps are normal**, not a failure: people travel, schedulers silently skip runs, life happens. The job is to notice and catch up.

- Widen the lookback to cover the whole gap plus a few days of margin.
- Say it out loud in the report: "Last sweep 12 days ago, so I looked back 15 days."
- **Work the oldest items first.** Postings expire, and the oldest are closest to expiring. Check posting dates before assuming something is still live.
- If the gap is very long, cover what you reasonably can, then say plainly how much older ground you did not cover. A silent partial catch-up reads exactly like a complete one.

A fixed lookback window cannot survive an outage longer than the window. Deriving it from the actual gap is what stops roles disappearing between runs.

## Step 1: Build the queries

For each track, expand into query variants using the track's archetypes **and the title-atlas variants** from onboarding (the same job wears different names; a search that misses the synonyms misses half the market).

**Always run two passes per track:**
1. **Location-scoped**, using their radius and locations.
2. **Function-wide remote**, if they accept remote work at all.

A location filter must never hide remote-eligible roles. This is not optional; it is the single most common way a sweep silently loses the best role in the market.

**If the user has more than one track, give them equal effort.** Count your queries per track and keep them level. Tracks drift out of balance easily, usually because one has louder job titles or a longer alias list, and the quieter track then looks like an empty market when it was really an unqueried one.

## Step 2: Sweep

Work through the primary channels in `my/channels.md` first, then secondary ones if the yield is thin. For each candidate role:

- **Open the posting.** Confirm it exists, is live, and is what the aggregator claimed. Aggregators relist dead and duplicated postings constantly.
- Capture: exact title, company, location and work mode, posted comp if stated publicly, the link you actually verified, and the posting date if visible.
- **Never write a row from a search-result snippet alone.**

Respect the sites you visit: normal browsing, no scraping at volume, nothing that violates a site's terms. Prefer the employer's own careers page over an aggregator when both exist, since it is authoritative and usually fresher.

### Never trust a search box to filter for you

Job-site search and API filters are frequently loose, semantic, or simply ignored. A query for "Director of Design" comes back with Director of Product Management and Director of Marketing; some employer APIs return the entire board no matter what you asked for, in no useful order. If you read the first twenty rows of that and stop, you get an unfiltered dump that looks exactly like a filtered result.

**So: treat any remote filter as a hint, never a result.** Pull the fuller list where you can, filter the titles yourself against the title atlas, and note the total you looked through. And **never report a search tool's emptiness as market signal**: "that job board's search cannot express this query" and "there are no such roles" are completely different statements, and only one of them should change what the user believes.

### When a source will not open

Work the ladder before giving up: the employer's own careers page, then a different route into the same site, then a plain fetch, then a browser if your harness has one. Then split the outcome honestly:

- **The site answered and the role is not there** , it is gone. Say so.
- **You could not get an answer either way** (login wall, blocked request, a page that renders nothing) , **this is not a dead role.** Keep it, flag it, hand the user the link. Per hard rule 8, never convert your own reach problem into a verdict about the job.

## Step 3: Filter and score

**Kill rules first (these end consideration, whatever else is good):**
- Trips a dealbreaker in `my/profile.md`.
- Location and work mode incompatible, and not remote-eligible.
- Requires work authorization the user does not have.
- Seniority clearly outside their range in either direction.
- Already in the tracker: **dedupe by company plus title, and by link.** Reposted roles are common; if a previously closed row reappears, mention it rather than silently re-adding it.

Every one of these needs **positive evidence**. "The posting says the office is required three days a week" is a kill. "I could not tell where it is based" is not, it is a flag.

**Then score fit 1 to 5** against the profile, with one or two lines of honest rationale:

- **5** , strong match on the core requirements, and something about it is genuinely interesting for this person.
- **4** , solid match, worth their time.
- **3** , plausible, with a real caveat named.
- **2 and below** , do not write the row. Say what you filtered and why, in one line, so they can correct your calibration.

Scoring inflation is the failure mode to avoid. If everything is a 4, the score carries no information and the user stops trusting it.

### Reputation and culture: read the trend, not a comment

Research what is publicly known about the employer and **report** it. Exclude a role only when it trips a culture dealbreaker the user named or falls below the tolerance they set during onboarding. Never quietly drop a role on culture the user did not ask you to enforce; some people are searching from strength and some need income soon, and that calibration is theirs.

When the user *has* asked you to filter on culture, hold a real standard before you kill anything:

1. **A single review is never enough**, however vivid. Look for a pattern across several independent reviews.
2. **Read the distribution, not the search snippet.** Search results surface the angriest sentences in a review base, which biases every judgment toward the kill.
3. **Weigh recency.** A bad cluster from three years ago against clean recent reviews describes a company that changed.
4. **Read the counter-evidence and say it too.** A verdict that only cites what supports it is an argument, not a verdict.
5. **Check who is complaining.** Problems concentrated in a department the user would never join are a caveat worth reporting, not a reason to drop the role.

**If you are unsure, write the row and say you are unsure**, with the quotes and the review count in the notes. Uncertain is a real answer and it belongs in front of the user. Killing is for the obvious cases.

## Step 4: Write the rows and present the batch

Write new rows as `Sourced` per `docs/pipeline.md`: role, company (linked to the verified homepage in Notion mode), track, fit score, fit notes, verified link, location with work mode, posted comp, date sourced.

**Then read the rows back before you report them.** Query what you just wrote and confirm every required field is populated, above all the link. A row the user cannot click is a row they cannot act on, which defeats the point of writing it. Tool success is not confirmation (hard rule 9); the read-back is.

Then present the batch compactly: role, company, fit score, one line of why, and the link. Say what you swept, what you filtered out and why, and where the yield was thin.

**Include a channel ledger.** One line per channel, with exactly one verdict:

- **SWEPT** , you actually queried it this run. Only then may you say what it produced, including "nothing".
- **SKIPPED** , you did not get to it. Say the word "skipped" and why.
- **BLOCKED** , you tried and could not get in. Name what failed.

Never describe the output of a channel you did not run. A skipped channel reported as an empty one tells the user a place has been looked that has not, which is worse than a thin sweep because they cannot see the hole.

**Include a "needs your eyes" section** whenever something is unresolved: roles you could not verify, employers where the culture read was genuinely uncertain, anything you flagged rather than killed. Every entry gets its link. If there is nothing, say so in one line.

Close with the actual next step:

> Approve the ones worth pursuing by moving them to Approved in your tracker, and I will build kits for them next time we talk.

Do not ask them to tell you which ones they approve. They click; you reconcile.

## Keep the channel plan alive

`my/channels.md` is the sweep's memory, not a static plan from onboarding. Each run, write back what you learned:

- **Channels that worked**, with roughly what they returned, so a future run can tell a quiet channel from a broken one.
- **Channels that would not open**, and what you tried. Keep these listed rather than deleting them; a source you cannot reach is a known gap, and removing it turns a visible hole into silence.
- **Sites the user should check by hand.** Some employers' listings are unreadable to an agent but perfectly usable by a person. Keep a short manual-check list in `my/channels.md` so the user can cover what you cannot, rather than never learning those roles existed.

## Step 5: Offer a recurring sweep

**Offer this the first time a sweep succeeds, and never nag about it again.**

A search dies from silence, not from bad roles. A standing sweep keeps the pipeline fed without the user having to remember. Ask what interval fits: daily suits an urgent search, weekly suits a quiet one, and those are the two that matter; take whatever they say.

Then set it up in whatever way their harness supports, checking what is available rather than assuming:

- **Claude Code** can schedule recurring work. Offer to create it, and tell them plainly where it will live and how to cancel it.
- **No scheduler available?** Say so, and give them the honest low-tech version: a calendar reminder that says "open Jobsmith, say sweep." That works, and pretending otherwise helps nobody.

Record what was set up, including the interval and how to change it, in `my/state.json` so a later session can answer "am I still running sweeps?"

**Rules for a scheduled sweep run:**
- It writes `Sourced` rows and reports. It never approves, tailors, or sends anything.
- **Record the run and its date in `my/state.json`, every time.** That record is what makes the Step 0 gap check possible. Scheduled runs get skipped silently more often than anyone expects, and without a trail there is no way to notice.
- If a run finds nothing, that is a valid, quiet result. Say so in one line; do not manufacture rows to look useful.
- If several consecutive runs find nothing, say that plainly and suggest revisiting the channel plan or widening the title atlas. Repeated empty sweeps are a channel problem, not a reason to lower the user's bar.

## Evaluating a single posting

When the user hands you one link instead of asking for a sweep: verify it is live, run the same kill rules and scoring, tell them the honest read including anything that concerns you, and offer to add it as a row. Their call whether it goes in.
