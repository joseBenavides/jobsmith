---
name: source
description: Sweep the user's channels for roles worth their time, score them honestly, and write new Sourced rows to the pipeline. Run when the user asks to source, sweep, or find roles, when they ask what is out there, or on a recurring schedule they set up. Also evaluates a single posting they hand you.
---

# Source

Find roles the user would actually want, and put them in front of them without wasting their attention. A sweep that returns twenty mediocre rows is worse than one that returns two good ones, because the user pays for every row in review time.

Read `AGENT.md` first. Hard rules apply, especially: never guess a URL, and never apply to anything.

## Inputs

- `my/profile.md` , tracks, locations, work modes, authorization, constraints, dealbreakers.
- `my/channels.md` , the researched channel plan per track, from onboarding.
- The tracker , to dedupe against what is already there.

**Missing channel plan?** Say so and offer to run the channel research step from onboarding first; a sweep without it is guesswork. If they would rather sweep now, use general search against their profile and mark the results as unresearched-channel finds.

## Step 1: Build the queries

For each track, expand into query variants using the track's archetypes **and the title-atlas variants** from onboarding (the same job wears different names; a search that misses the synonyms misses half the market).

**Always run two passes per track:**
1. **Location-scoped**, using their radius and locations.
2. **Function-wide remote**, if they accept remote work at all.

A location filter must never hide remote-eligible roles. This is not optional; it is the single most common way a sweep silently loses the best role in the market.

## Step 2: Sweep

Work through the primary channels in `my/channels.md` first, then secondary ones if the yield is thin. For each candidate role:

- **Open the posting.** Confirm it exists, is live, and is what the aggregator claimed. Aggregators relist dead and duplicated postings constantly.
- Capture: exact title, company, location and work mode, posted comp if stated publicly, the link you actually verified, and the posting date if visible.
- **Never write a row from a search-result snippet alone.**

Respect the sites you visit: normal browsing, no scraping at volume, nothing that violates a site's terms. Prefer the employer's own careers page over an aggregator when both exist, since it is authoritative and usually fresher.

## Step 3: Filter and score

**Kill rules first (these end consideration, whatever else is good):**
- Trips a dealbreaker in `my/profile.md`.
- Location and work mode incompatible, and not remote-eligible.
- Requires work authorization the user does not have.
- Seniority clearly outside their range in either direction.
- Already in the tracker: **dedupe by company plus title, and by link.** Reposted roles are common; if a previously closed row reappears, mention it rather than silently re-adding it.

**Then score fit 1 to 5** against the profile, with one or two lines of honest rationale:

- **5** , strong match on the core requirements, and something about it is genuinely interesting for this person.
- **4** , solid match, worth their time.
- **3** , plausible, with a real caveat named.
- **2 and below** , do not write the row. Say what you filtered and why, in one line, so they can correct your calibration.

Scoring inflation is the failure mode to avoid. If everything is a 4, the score carries no information and the user stops trusting it.

**Reputation and culture:** research what is publicly known about the employer and **report** it. Exclude a role only when it trips a culture dealbreaker the user named or falls below the tolerance they set during onboarding. Never quietly drop a role on culture the user did not ask you to enforce; some people are searching from strength and some need income soon, and that calibration is theirs.

## Step 4: Write the rows and present the batch

Write new rows as `Sourced` per `docs/pipeline.md`: role, company (linked to the verified homepage in Notion mode), track, fit score, fit notes, verified link, location with work mode, posted comp, date sourced.

Then present the batch compactly: role, company, fit score, one line of why, and the link. Say what you swept, what you filtered out and why, and where the yield was thin. Close with the actual next step:

> Approve the ones worth pursuing by moving them to Approved in your tracker, and I will build kits for them next time we talk.

Do not ask them to tell you which ones they approve. They click; you reconcile.

## Step 5: Offer a recurring sweep

**Offer this the first time a sweep succeeds, and never nag about it again.**

A search dies from silence, not from bad roles. A standing sweep keeps the pipeline fed without the user having to remember. Ask what interval fits: daily suits an urgent search, weekly suits a quiet one, and those are the two that matter; take whatever they say.

Then set it up in whatever way their harness supports, checking what is available rather than assuming:

- **Claude Code** can schedule recurring work. Offer to create it, and tell them plainly where it will live and how to cancel it.
- **No scheduler available?** Say so, and give them the honest low-tech version: a calendar reminder that says "open Jobsmith, say sweep." That works, and pretending otherwise helps nobody.

Record what was set up, including the interval and how to change it, in `my/state.json` so a later session can answer "am I still running sweeps?"

**Rules for a scheduled sweep run:**
- It writes `Sourced` rows and reports. It never approves, tailors, or sends anything.
- If a run finds nothing, that is a valid, quiet result. Say so in one line; do not manufacture rows to look useful.
- If several consecutive runs find nothing, say that plainly and suggest revisiting the channel plan or widening the title atlas. Repeated empty sweeps are a channel problem, not a reason to lower the user's bar.

## Evaluating a single posting

When the user hands you one link instead of asking for a sweep: verify it is live, run the same kill rules and scoring, tell them the honest read including anything that concerns you, and offer to add it as a row. Their call whether it goes in.
