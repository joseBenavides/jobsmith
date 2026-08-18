# Using Jobsmith

One page, everything you need. You don't have to memorize any of this: Jobsmith offers the next step whenever you check in, and you can always just ask "what can you do?"

## The loop

Your search runs through a pipeline. Each opportunity is one row, and the row's status tells both of you whose move it is:

| Status | What it means | Whose move | What usually happens next |
|---|---|---|---|
| Sourced | Jobsmith found it and thinks it is worth your look | **Yours** | Review it; drag it to Approved, or close it as `passed` |
| Approved | You said "pursue this" | Jobsmith's | It builds the application kit next time you talk |
| Tailored | Your kit is drafted and waiting | **Yours** | Review the kit; when you send the application, mark it Applied |
| Applied | You sent it | Theirs | Jobsmith tracks follow-ups; you update when anything happens |
| Interviewing | Interviews scheduled or underway | Both | Prep support; log what happens |
| Offer | An offer is in hand | **Yours** | Negotiation support |
| Closed | Over, for any reason | | Always set the reason; patterns in reasons teach the search |

You make moves by editing the tracker directly: drag a card in Notion or edit the CSV. You never have to announce a change; Jobsmith reads the tracker every time a session starts.

## Things you can say

**Checking in (the daily driver):**
- "Where do things stand?" or just "hi" - you get the brief: what changed, what's due, what's waiting on you
- "Anything due this week?"

**Finding roles:**
- "Run a sweep" - search your channels for new roles
- "What do you think of this posting? <link>"

**Approved roles becoming applications:**
- "Build the kits for the approved roles"
- "Tailor for this JD: <link>" (works even for a role that isn't in the tracker yet)

**Your materials:**
- "Let's work on my brag doc" (or continue where you left off)
- "Update my profile: I'm now open to relocation"
- "Show me where that resume claim comes from" - every line traces to a source

**Understanding Jobsmith:**
- "What can you do?"
- "What does Tailored mean?"
- "Where does my data live?" (short answer: the `my/` folder, and nowhere else)

If a flow gets interrupted mid-conversation, nothing is lost. Jobsmith keeps its place and offers to resume next time.

## Your files

Everything about you lives in `my/` (git ignores it; delete it and Jobsmith knows nothing). The ones you'll actually open: `profile.md` (your targets and constraints), `brag-doc.md` (your master accomplishments), `channels.md` (where your field's jobs get posted), `kits/` (one folder per application), and `pipeline.html` (your dashboard, if you're not using Notion).

## The rules Jobsmith lives by

- **It never applies or sends anything.** You review, you send. Always.
- **It never invents a claim.** Every resume line traces to your materials or your own words. It will decline to write something that is not true, and it will tell you why.
- **It never guesses a link.** Every URL it gives you was verified live.
- **Your data stays local.** Nothing is transmitted anywhere except to the LLM you run it with.
