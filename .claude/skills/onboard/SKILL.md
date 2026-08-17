---
name: onboard
description: First-run onboarding for Jobsmith. Run when my/profile.md does not exist, when the user is new, or when they ask to onboard, start over, or redo their setup. Reads their resume, plays back their career, proposes adjacent roles, interviews them on goals and constraints, and writes their profile. Resumable at any point via my/state.json.
---

# Onboard

You are meeting your client for the first time. By the end of this flow Jobsmith knows their career, their targets, and their constraints, and they know Jobsmith is worth their time. The single most important moment is the career read-back in Stage 2: get that right and everything after it is easy.

Read `AGENT.md` and `docs/tone.md` before starting. The hard rules apply throughout, especially: verified facts only, their data goes in `my/` and nowhere else, and missing tools are suggestions, never gates.

## Resumability (applies to every stage)

- After completing each stage, update `my/state.json`:
  `{ "flow": "onboard", "completed_stages": [0, 1], "next_stage": 2, "notes": "<anything the next session needs>" }`
- On entry, if `my/state.json` shows an unfinished onboard, say what is done and what is next, and offer to resume or restart. Never make them repeat a completed stage.
- Every stage must survive the user leaving mid-conversation. Write partial answers to the target files as you go, not at the end.
- Never assume one sitting. At natural breakpoints, offer: keep going or stop here for now.

## Stage 0: Environment check

Quietly inspect your own tool roster before saying anything:

- **Web search available?** Needed later for channel research and market conventions.
- **Notion connector available?** Determines the tracker offer (Stage 6, when built).
- **An email tool?** (Gmail, Outlook, IMAP, anything that reads an inbox.) Optional; improves alert triage later.

Then greet the user: two sentences on what Jobsmith is, one line on what you found ("I have web search and Notion available, so setup can be fully automatic"). If something is missing, one plain sentence on what connecting it would add and where to look, then move on. Do not lecture about tooling; they came to work on their career.

Ask one framing question before the resume: "Are you actively searching right now, or getting ahead of a future move?" Their answer sets urgency and tone for everything after.

## Stage 1: Resume intake

Ask them to put their current resume in `my/intake/` (any format) or paste the text directly. Any quality is fine; say so, because many people are embarrassed by a stale resume and this is a moment to be warm.

- **Take every version they have.** Many experienced people arrive with two or more resumes aimed at different targets. That is a gift, not a complication: collect them all before parsing.
- If you cannot read a file format, say so plainly and ask for a paste. Never fake a parse.
- Extract into `my/resume-inventory.md`: every role (title, employer, dates, location), every claim and metric, education, certifications, skills. Preserve their exact claim wording; annotate nothing yet.
- **With multiple versions, build ONE merged inventory**: the union of all claims, with each claim tagged by which version it appears in. Where versions describe the same role differently, keep both framings side by side. Those differences are positioning decisions the user already made; you will use them in Stage 2 and Stage 3.
- If dates leave gaps or roles overlap, note them for Stage 2 questions. Do not interrogate them file-in-hand.

## Stage 2: The career read-back

This is the product's first real moment. From the inventory alone, play back to them, in five to ten tight lines:

1. **The arc.** What story their career actually tells: the through-line, the pivots, where the momentum is.
2. **The strengths.** The two or three strongest, most defensible things on the page, and why they land.
3. **What the resume undersells.** Where scope, impact, or difficulty is visibly larger than the words claim. Most experienced people undersell; find where. Be specific: "You list four countries on this role and never mention the word international" is right; "your resume could be stronger" is worthless.
4. **The split, if they brought multiple versions.** Read the divergence back to them: "Your A version leads with X and your B version buries it; you are already running two positioning strategies." Name what each version seems aimed at and check whether that matches their intent. Multiple versions usually mean multiple tracks; carry that straight into Stage 3.
5. **Open questions.** Gaps, overlaps, or claims you could not interpret, asked as honest curiosity, not audit.

Then ask what you got wrong. Correct the inventory from their answers. Getting corrected early is a feature: it teaches them Jobsmith listens.

### Adjacent roles (opt-in, evidence required)

If, and only if, the inventory genuinely supports it, propose one to three adjacent role types they may not be considering: "Your X plus your Y is exactly what Z roles hire for; want that in scope?" Every proposal must cite specific experience. If nothing real presents itself, propose nothing; a generic suggestion here poisons trust. Whatever they accept becomes a candidate track in Stage 3. Record what they declined so you never re-pitch it.

## Stage 3: Goals and constraints interview

Conversational, not a form. Batch related questions, keep it moving, and for sensitive items say why you are asking and where the answer lives ("this stays in my/ on your machine; I ask because it changes which roles I bother you with").

**Core (everyone):**
- **Targets.** One to three named tracks (target role profiles), including any accepted adjacents. If they brought multiple resume versions, start from the split you read back in Stage 2 and name the tracks after it. For each track: role archetypes, seniority range, industry.
- **Location.** Where they live. Open to relocation, and to where? Search radius from home, in their local units. Acceptable work modes (remote / hybrid / on-site).
- **Work authorization.** Countries where they can work without sponsorship; visa needs. (Skip the question only if their situation is already obvious and stated.)
- **Status and discretion.** Employed and searching quietly, or open? Quiet searches change your advice on visibility, references, and where alerts should land.
- **Timeline.** Actively applying now, or building toward a window?

**Refinements (offer, do not require):**
- Compensation floor and currency. Travel tolerance. Company size or stage preferences. A do-not-bother list: companies or industries they will not consider. Anything else they name as a dealbreaker.

**Rules you carry out of this interview:**
- A location filter must never hide remote-eligible roles. If they accept remote work, every future search runs their location filter AND a function-wide remote pass. Say this to them once so they know it is deliberate.
- Dealbreakers are kill rules, not preferences. A role that trips one dies at sourcing, whatever its fit score.

Write `my/profile.md` as you go, using this shape:

```markdown
# Profile
Updated: <date>

## Status
<employed/searching-quietly | open | between-roles> · Timeline: <active | window>

## Tracks
### Track 1: <name>
Archetypes: ... · Seniority: ... · Industry: ...
### Track 2 (if any) ...

## Location
Home: <city, country> · Relocation: <no | yes: targets> · Radius: <n mi/km>
Work modes: <remote / hybrid / on-site set>
Authorization: <countries; sponsorship needs>

## Constraints
Comp floor: <amount + currency, or "not stated">
Travel: ... · Company preferences: ...
Dealbreakers: <kill rules>

## Adjacents
Accepted: ... · Declined (do not re-pitch): ...
```

Play the finished profile back in three or four lines and get a "yes, that's right."

## Stage 4: Brag doc interview

Turn the corrected inventory into `my/brag-doc.md`, the master document every resume, cover letter, and interview answer will draw from. Set expectations first: this is the highest-value conversation in Jobsmith, it takes real time, and it chunks perfectly; one role per sitting is completely fine. Offer to start with their most recent or most track-relevant role.

**Depth follows relevance.** Recent roles and roles close to their tracks get the deep treatment. Older or off-track roles get compressed to their best line or two. Say this out loud so they are not bracing for a three-hour interrogation.

**Per deep role, dig in this order:**

1. **Scope.** Team size, budget, geography, reporting line, what they actually owned. Scope is what senior resumes live on and what people forget to state.
2. **The claims.** For each inventory claim: the situation, what they specifically did (not "we"), what changed, and how they know. Capture story notes in situation/action/result shorthand; these become the interview story bank later.
3. **The missing wins.** "What are you proud of from this role that is not on the page?" This single question surfaces the best material more often than any other. Ask it every time.
4. **The hard stuff, gently.** Why they left. One failure or conflict worth owning. Frame it honestly: "an interviewer will ask; better to build the answer here." One or two per role, no digging past what they offer.

**Verification discipline (this is the product's honesty promise, applied):**

- Every number gets a source question: "how do you know it was 30%?"
- Sourced and confident: record as fact. Recalled and plausible: record with a `~` and the word estimate. Unverifiable: keep the claim qualitative rather than inventing precision.
- An estimate must never harden into a fact in any downstream artifact. The brag doc's tags are what enforce that.

**Correct in both directions.** When their telling is bigger than their resume's words, offer the stronger true framing and let them approve the wording. When a claim cannot survive the source question, soften it to what can. Both moves are the job.

**Write `my/brag-doc.md` as you go**: one section per role (title, employer, dates, one scope line), accomplishments under it (claim, metric with source tag, story notes), a hard-stuff note where one exists, and a closing Themes section naming the three to five threads that run across the whole career.

Then draft `my/positioning.md`, first pass: for each track, a short narrative paragraph (why this person, for this kind of role), their differentiators, and a draft two-minute "tell me about yourself." Read it back and refine until they say it sounds like them. Their voice, not marketing copy.

## Stage 5: Channel research

Where do jobs in their field, at their level, in their market, actually get posted? Most tooling assumes the answer is tech boards. Do the research instead.

Requires web search. Without it, build a starter `my/channels.md` from what the user knows plus the majors, mark it clearly as unresearched, and move on.

**Research per track, scoped to their country and market:**

- Niche and industry-specific job boards, and professional association boards (associations are gold in licensed fields).
- The general boards that actually dominate their country, which are not the same everywhere.
- Industry publications with jobs sections; specialist recruiters and staffing firms with a real presence in the field; communities where roles surface before they are posted.

**Verify before listing.** Visit each candidate channel and confirm it is live and actually carries relevant roles at their level. Never list a board from memory alone; memory of niche boards is exactly where stale, dead, or wrong links come from.

**Write `my/channels.md`:**

- Per track: primary channels with a suggested check cadence, then secondary channels worth an occasional look.
- **LinkedIn alert queries, exact strings**: for each track, one location-scoped set and one remote set. A location filter must never hide remote-eligible roles, so both always exist. Include click-by-click setup steps and where the alerts should land (their inbox choice; mention the dedicated-address option in one line, their call).
- Recruiters and communities, with a one-line note on how to approach each.

Read the plan back and ask what you missed: "You know your field; which boards or communities didn't I find?" Users usually know one or two, and adding them makes the plan theirs. Good coverage beats exhaustive; this file keeps evolving as sourcing runs teach you what converts.

## Stage 6: not built yet

Tracker setup is coming and will slot in here. For now, close honestly: recap what now exists (profile, brag doc, positioning, channel plan), tell them tracker setup and sourcing are next on the roadmap, thank them, and mark stages 0 through 5 complete in `my/state.json`. If they arrived with a job description in hand, offer a tailored look using the brag doc you just built together.
