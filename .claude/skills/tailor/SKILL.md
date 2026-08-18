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
- Writing rules from `AGENT.md` apply in full.

**`resume.html`** , generated from `assets/resume-template.html`: single column, standard headings, machine-readable. The user can print to PDF from any browser. Keep the template's draft banner, filled in with this kit's open items, until the user clears the kit to send; it is visible on screen and never prints.

**Length is a hard constraint, and you must measure it, not eyeball it.** Default target is two pages. Markdown length tells you nothing about pagination, so count the rendered pages before showing the user anything:

```
msedge --headless --disable-gpu --print-to-pdf="out.pdf" --no-pdf-header-footer "file:///<abs-path>/resume.html"
```

(Or any headless browser; Chrome takes the same flags.) Count the pages in the PDF. Over target means cut the least relevant material, never shrink fonts or margins. Do not ship a resume sitting exactly on a page boundary; leave margin. If you genuinely cannot render, say so plainly and tell the user the page count is unverified rather than assuming it fits.

**`cover-letter.md`** , the highest AI-tell risk in the whole product. A polished-but-generic letter reads as machine-written and gets screened out; voice is a requirement here, not a nicety.

- **Voice sources, in order:** samples in `my/voice/`, the learned profile in `my/voice-notes.md`, then `my/positioning.md`. If none exist, run first-letter calibration before drafting anything.
- **First-letter calibration** (first kit, or no voice sources yet). Offer two paths and let them pick:
  1. *They draft, you edit.* They write a rough version in their own words, however clumsy; you tighten it without sanding their voice off. This gives the strongest signal.
  2. *You draft two, they react.* Two deliberately different versions, then walk the key lines together: "Would you say this sentence out loud? Which words here would you never use?" Iterate until they say "I would send this."
- **Learn and persist.** Whatever calibration teaches goes in `my/voice-notes.md`: phrases they actually use, words they would never say, sentence rhythm, formality level. Every later letter starts from that file, and every edit they make to any letter updates it. Letters should converge on their voice over time, not stay at first-draft distance.
- **Tell-check before presenting.** Scan your own draft for AI tells: em dashes (already banned), "not just X but Y" constructions, "I am excited to", generic flattery, three-part crescendos, and any sentence on the user's never-say list. Then read it once as the hiring manager: if the letter could have been written about any candidate, rewrite it.
- Content rules stay: under a page, roughly 300 words, one verified company fact that explains why this role, two or three proof points mapped to the JD's top needs, gaps addressed briefly and without apology. No restating the resume.
- When presenting, say it plainly: read this aloud once before sending; anything that catches in your mouth, we change.

**`log.md`** , the kit's interaction log, started now: date, JD link, contacts known at this company, and a running record of what happens (sent when, replies, interviews). This file is the per-role CRM.

## Step 3: Review with the user

Present the kit with a short summary of choices: what leads and why, what was left out, how each gap was handled. Offer a source check: any line they question maps back to its inventory or brag-doc entry on request. Revise until they approve it. Approval of the kit is not permission to send anything; they send.

## Step 4: Close the loop

On their approval:
- Flip the pipeline row to `Tailored`. Set Next Action ("apply via <channel>") and a Next Action Date a few days out.
- When they say they sent it, or reconcile detects it, the row moves to `Applied` with Date Applied, and `log.md` records it.

If they asked for changes you could not honor (a claim that is not true, a number that is not verified), the kit ships without it and the log records why. The resume that gets the interview has to survive the interview.
