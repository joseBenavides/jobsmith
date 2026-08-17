---
name: tailor
description: Turn a job description into a complete application kit, a tailored resume and cover letter drafted from the user's verified materials. Run when a pipeline row reaches Approved, when the user provides a job description or posting link, or when they ask to tailor or apply for a role. Drafts only; the user reviews and sends everything.
---

# Tailor

An Approved row is a work order. This module turns it into a kit the user can review, approve, and send themselves. The bar: every line survives an interview, and the whole kit reads like the user on their best day, not like software.

Read `AGENT.md` first. The hard rules bind every artifact here, especially: verified facts only, never guess a URL, never send or apply, and the candidate-facing writing rules.

## Inputs

- **Preferred: an Approved pipeline row.** Its Link is the JD. Verify the posting is still live before building; if it died, tell the user and offer to close the row (`position-pulled` or `stale`).
- **Also fine: a pasted JD or posting link** with no row yet. Offer to add the row (as `Approved`, since the user's ask is the approval).
- Load `my/profile.md`, `my/resume-inventory.md`, `my/brag-doc.md`, and `my/positioning.md`.
- **Soft prerequisite, never a block:** without a brag doc, say plainly that tailoring from the inventory alone works but a brag-doc session makes it much stronger, then proceed with whichever they choose.

## Step 1: Decode the JD

Before writing a word of resume:

1. Snapshot the posting text to `my/kits/<company-role-slug>/jd.md`. Postings die; the kit keeps its own copy, with the link and the date captured.
2. Extract what the role actually wants: the top requirements in priority order (the JD's order is often not its real priority), seniority and scope signals, and the exact terms an ATS or screener will scan for.
3. Map each requirement to the user's evidence: which inventory or brag-doc entries prove it.
4. **Name the gaps.** Requirements with no evidence get listed honestly, with a strategy each: address in the cover letter, reframe truthfully from adjacent experience, or accept as a real gap. Never paper over a gap with vague language.

If decoding reveals a dealbreaker or a bad fit the user may not have seen (a culture finding, seniority mismatch, location conflict), say so now, before the work. Building a beautiful kit for the wrong role helps no one. Their call whether to proceed.

## Step 2: Build the kit

Everything goes in `my/kits/<company-role-slug>/`:

**`resume.md`** , the tailored resume:
- Select, reorder, and reweight from the master materials. Never invent, never inflate. Tailoring means choosing which true things lead, not creating new ones.
- Mirror the JD's terminology only where it is truthful ("revenue strategy" for "revenue management" is fine if that is what they did; a title change is not).
- Claims tagged `~estimate` in the brag doc stay visibly approximate or get dropped; they never harden into precise facts here.
- Length is a hard constraint: fit the target page count (default two pages) with margin, by cutting the least relevant material, not by shrinking fonts.
- Writing rules from `AGENT.md` apply in full.

**`resume.html`** , generated from `assets/resume-template.html`: single column, standard headings, machine-readable. The user can print to PDF from any browser.

**`cover-letter.md`**:
- Short: under one page, roughly 300 words.
- Specific: one verified fact about the company that explains why this role (researched this session, link verified), then two or three proof points mapped to the JD's top needs, in the user's voice per `my/positioning.md`.
- No AI tells, no flattery, no restating the resume. If a gap from Step 1 needs addressing, address it here, briefly and without apology.

**`log.md`** , the kit's interaction log, started now: date, JD link, contacts known at this company, and a running record of what happens (sent when, replies, interviews). This file is the per-role CRM.

## Step 3: Review with the user

Present the kit with a short summary of choices: what leads and why, what was left out, how each gap was handled. Offer a source check: any line they question maps back to its inventory or brag-doc entry on request. Revise until they approve it. Approval of the kit is not permission to send anything; they send.

## Step 4: Close the loop

On their approval:
- Flip the pipeline row to `Tailored`. Set Next Action ("apply via <channel>") and a Next Action Date a few days out.
- When they say they sent it, or reconcile detects it, the row moves to `Applied` with Date Applied, and `log.md` records it.

If they asked for changes you could not honor (a claim that is not true, a number that is not verified), the kit ships without it and the log records why. The resume that gets the interview has to survive the interview.
