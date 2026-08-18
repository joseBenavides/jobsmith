# Architecture

How Jobsmith is put together, and why. If you are evaluating this repo rather than using it, start here.

## The thesis

Most AI job-search tools are web applications with a model behind them. That shape forces three compromises: your career data lives on someone else's server, you get whatever model the vendor chose, and the product can only do what its UI exposes.

Jobsmith inverts that. It is **an agent definition plus a set of skills, run by an agent harness you already have, against files on your own disk.** There is no server, no account, and no database. The consequences are the product:

- Your data is local. Deleting one folder deletes everything Jobsmith knows.
- The model is yours to choose. The skills are markdown, not vendor-locked code.
- The interface is conversation plus your own files, so capability is not bounded by a screen someone designed.

The cost is a real dependency: you need an agent harness. That is the trade this project accepts.

## The four layers

```
  AGENT.md          identity, hard rules, routing        (always loaded)
      |
  skills/*.md       one file per workflow                (loaded on demand)
      |
  docs/*.md         contracts and reference              (loaded when relevant)
      |
  my/               the user's data and state            (never tracked in git)
```

**AGENT.md** is the constitution: who the agent is, the rules it cannot break, how it behaves on a first run versus a returning one, and what modules exist. It is deliberately short. Rules that must never be missed live here; everything else is a reference the agent reads when it needs it.

**Skills** are workflows. Each is a single markdown file with frontmatter describing when it applies, so a harness can select it. They are written as procedures with judgment built in, not scripts: what to do, in what order, what to refuse, and what to tell the user.

**Docs** are the contracts. `pipeline.md` defines the data model both tracker modes implement. `tone.md` governs register. `philosophy.md` records design positions so contributors do not undo them by accident. Splitting contracts from workflows means two skills that touch the pipeline cannot drift apart.

**`my/`** is the entire state of a search: profile, brag doc, positioning, channels, voice samples, tracker, kits, and a resume-point file. It is gitignored, so updating the product with `git pull` never touches user data, and user data can never leak into a commit.

## State and resumability

Job searching happens in interrupted fragments, so no flow may assume one sitting.

- `my/state.json` records the flow in progress, completed stages, what is next, and notes for the next session.
- Flows write partial output as they go rather than at the end.
- On entry, the agent reads state and offers to resume before anything else.

The same file is how the agent tolerates being a different process each time: a session is stateless, but the search is not.

## The pipeline is the data model, not a wizard

`Sourced -> Approved -> Tailored -> Applied -> Interviewing -> Offer -> Closed`

Two design choices matter more than the states themselves:

**Approval is a status change the user makes, not a message they send.** The user edits the tracker directly; the agent reconciles at session start. This keeps the human gate real (nothing proceeds without a deliberate act) while removing the bookkeeping tax of narrating changes to an AI.

**Terminal rows carry an outcome.** A closed row without a reason teaches nothing. With reasons, the pipeline becomes a diagnostic: repeated `rejected-at-screen` on one track points at the resume, repeated `rejected-after-interview` points at prep.

Modules are independently invokable and declare **soft prerequisites**: tailoring works without a brag doc, says plainly that it would be stronger with one, and offers to backfill. Nothing blocks.

## Degradation instead of requirements

Every capability has a working path with no account, no API key, and no specific model:

| Capability | Preferred | Degraded |
|---|---|---|
| Tracker | Notion database, created for the user | `pipeline.csv` plus a generated HTML dashboard |
| Channel research and sourcing | Harness web search | User-supplied postings and links |
| Resume output | Markdown plus ATS-safe HTML | Same; PDF via the user's own browser |
| Email triage | Any inbox the harness can read | User pastes or forwards |

Missing capability produces a suggestion, never a wall. This is what makes "works with any harness" true rather than aspirational.

## Guardrails, and why they are layered

The hard rules in `AGENT.md` are the ones a violation of which would damage the user: never send on their behalf, never invent a claim, never guess a URL, keep their data in `my/`. They are stated at the top of the always-loaded file because a rule buried in a skill is a rule that fails when a different skill is running.

Skill-level rules are narrower and procedural: measure the resume page count by rendering it, snapshot a posting before it disappears, verify a job is still live before building a kit, run a tell-check before showing a cover letter. These live with the workflow they constrain.

The pattern is deliberate: **invariants at the top, procedures next to the work.** Several of these exist because an end-to-end test caught the failure first, which is the honest way to arrive at a guardrail.

## Extending it

A new module is a new markdown file in `.claude/skills/<name>/SKILL.md` with frontmatter, plus a row in the AGENT.md module table. If it touches pipeline state, it implements the contract in `docs/pipeline.md` rather than inventing its own fields. If it produces candidate-facing text, the writing rules in `AGENT.md` apply, and voice comes from `my/voice/`.

The test for a new capability is not whether it works in the ideal setup. It is whether it degrades honestly when the ideal setup is missing.
