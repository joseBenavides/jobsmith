# Jobsmith

Your AI career agent. Jobsmith runs your job search the way a good talent agent would run it: it learns your career, builds your case, finds where the real openings in your field live, tailors every application, and preps you for the interviews. You make every call. It drafts, you approve, you send.

Jobsmith is not an app or a service. It is an agent definition plus a set of skills that run inside an AI coding agent such as Claude Code, on your machine, with your files. There is no server, no account, and no one between you and your search.

> **Status: early release.** The core is built and working: onboarding, brag doc, industry channel research, pipeline tracking, and tailored application kits. Sourcing sweeps, interview prep, and negotiation are next. Expect rough edges, and please open an issue when you hit one.

## Who it's for

Experienced professionals in any industry. Nurses, attorneys, engineers, marketers, designers, operators, executives. If you have a resume and real work experience behind it, Jobsmith is built for you.

It is not built for first-job seekers. Starting a career is a different problem with different needs, and a tool that tries to serve everyone serves no one well.

## What makes it different

- **It never applies or sends anything for you.** Auto-apply tools flood recruiters and get candidates quietly filtered out. Jobsmith is the opposite bet: fewer, better applications, each one reviewed and sent by you.
- **It refuses to inflate.** The brag doc interview digs hard for the impact you undersell, because most experienced people undersell. It will not invent or embellish a claim you couldn't defend in an interview.
- **It knows your industry's channels.** Most job tools assume everyone works in tech. During onboarding, Jobsmith researches where roles in your specific field actually get posted and writes you a personal channel plan.
- **Your data stays yours.** Everything about you lives in one local folder, `my/`. Nothing phones home. Delete the folder and Jobsmith knows nothing about you.
- **Quiet by design.** Most people search while employed. Jobsmith runs entirely on your machine and its guidance covers the practical side of a discreet search.

## How it works

Your search is tracked as a pipeline:

`Sourced -> Approved -> Tailored -> Applied -> Interviewing -> Offer -> Closed`

The pipeline is the data model, not a forced path. Every module works on its own, and you enter wherever you need:

| Module | What it does |
|---|---|
| Onboard | First-run setup: reads your resume, interviews you about goals, researches your industry's channels, sets up your tracker |
| Brag doc | A structured interview that turns your experience into a master document of defensible accomplishments |
| Source | Sweeps your channel plan for roles worth your time, scores them honestly, and can run on a schedule you set |
| Tailor | Takes a job description, produces a tailored resume and cover letter kit for your approval |
| Interview prep | Company research and likely questions mapped to your real stories (not built yet) |
| Negotiate | Offer analysis and negotiation prep (not built yet) |

You manage the pipeline by clicking, not by chatting. With Notion connected, your pipeline is a filtered table you toggle directly; without it, a simple spreadsheet file does the same job. Jobsmith reads your changes at the start of each session.

## Requirements

1. **An AI agent harness.** [Claude Code](https://claude.com/claude-code) is recommended and first-class. Other harnesses and models work too; see `docs/other-harnesses.md`.
2. **A resume.** Any state, any quality. It is the seed everything grows from.
3. **Notion, recommended but optional.** With the Notion connector, Jobsmith creates your pipeline tracker for you. Without it, you get a local spreadsheet file instead.

## Quickstart

**1. Install Claude Code.** Follow [Anthropic's install guide](https://code.claude.com/docs/en/overview). Note that Claude Code requires a paid Claude plan (Pro or above); the free tier does not include it.

**2. Get Jobsmith onto your machine.** Either clone it:

```
git clone https://github.com/joseBenavides/jobsmith.git
```

or use the green **Code** button above, choose **Download ZIP**, and unzip it wherever you keep documents. No git required. (The unzipped folder is named `jobsmith-main`; rename it to `jobsmith` if you want the commands below to match exactly.)

**3. Put your resume in the `my/intake/` folder.** Any format, any state. If you have more than one version, add them all; the differences are useful.

**4. Open the folder in Claude Code and say hello.**

```
cd jobsmith
claude
```

Then type `hello`. Jobsmith notices it hasn't met you, checks what tools it has, and offers to start onboarding. Expect the first conversation to take a while, and know that you can stop at any point and pick up later; nothing is lost.

**Optional but recommended: connect Notion** before step 4. With it, Jobsmith builds your pipeline tracker for you as a real database with filtered views. Without it, you get a spreadsheet file and a dashboard, which work fine. See [Notion's MCP setup guide](https://www.notion.com/help/notion-mcp) or ask Jobsmith to walk you through it. One gotcha worth knowing: after connecting, you must explicitly grant access to the pages Jobsmith should see.

Once you're running, [Using Jobsmith](docs/using-jobsmith.md) is the one page worth reading: the pipeline loop, whose move each status is, and example things you can say. You don't need to memorize any of it; Jobsmith offers the next step whenever you check in, and "what can you do?" always works.

## How it's built

[Architecture](docs/ARCHITECTURE.md) covers the design: the four layers, how state survives interrupted sessions, why the pipeline is a data model rather than a wizard, how every capability degrades instead of requiring, and why the guardrails are layered the way they are. [Philosophy](docs/philosophy.md) records the design positions behind it.

## Using a different AI

Claude Code is what Jobsmith is developed and tested against. The skills are plain markdown, so other agent tools (and other models) can run them; see [other harnesses](docs/other-harnesses.md) for what any harness needs and how to adapt.

## Privacy

Your profile, brag doc, pipeline, and every generated artifact live in `my/`, which is ignored by git. Nothing in this repository ever contains your personal data, and nothing is transmitted anywhere except to the LLM you chose to run it with.

## License

MIT. See [LICENSE](LICENSE).
