# Jobsmith

Your AI career agent. Jobsmith runs your job search the way a good talent agent would run it: it learns your career, builds your case, finds where the real openings in your field live, tailors every application, and preps you for the interviews. You make every call. It drafts, you approve, you send.

Jobsmith is not an app or a service. It is an agent definition plus a set of skills that run inside an AI coding agent such as Claude Code, on your machine, with your files. There is no server, no account, and no one between you and your search.

> **Status: pre-release.** Jobsmith is being built in the open and is not ready to use yet. Watch or star the repo to catch the launch.

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
| Tailor | Takes a job description, produces a tailored resume and cover letter kit for your approval |
| Source | Sweeps your channel plan for roles worth your time |
| Interview prep | Company research and likely questions mapped to your real stories |
| Negotiate | Offer analysis and negotiation prep |

You manage the pipeline by clicking, not by chatting. With Notion connected, your pipeline is a filtered table you toggle directly; without it, a simple spreadsheet file does the same job. Jobsmith reads your changes at the start of each session.

## Requirements

1. **An AI agent harness.** [Claude Code](https://claude.com/claude-code) is recommended and first-class. Other harnesses and models work too; see `docs/other-harnesses.md`.
2. **A resume.** Any state, any quality. It is the seed everything grows from.
3. **Notion, recommended but optional.** With the Notion connector, Jobsmith creates your pipeline tracker for you. Without it, you get a local spreadsheet file instead.

## Quickstart

Not yet. This section will be real at launch. The short version will be: install Claude Code, download this folder, open it, and say hello. Jobsmith notices it hasn't met you and takes it from there.

## Privacy

Your profile, brag doc, pipeline, and every generated artifact live in `my/`, which is ignored by git. Nothing in this repository ever contains your personal data, and nothing is transmitted anywhere except to the LLM you chose to run it with.

## License

MIT. See [LICENSE](LICENSE).
