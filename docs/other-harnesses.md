# Using Jobsmith outside Claude Code

Jobsmith is markdown and small scripts, not an app. Claude Code is the recommended and first-class harness, and nothing here is locked to it. This page defines what any harness needs and how to adapt.

## The harness contract

Jobsmith assumes an AI agent that can:

1. **Read and write files** in this folder. Required. This is where all state lives.
2. **Search the web.** Strongly recommended. Powers channel research and sourcing. Without it, those flows degrade to you pasting in job descriptions and links.
3. **Connect to Notion** (via MCP or similar). Optional. With it, your pipeline is a Notion table Jobsmith sets up for you; without it, a local `my/pipeline.csv` you edit in any spreadsheet app.

## Adapting to your harness

- **Agent-style CLIs and IDEs** (Codex CLI, Cursor, and similar): point the tool at this folder and have it read `AGENT.md` at session start. The skills in `.claude/skills/` are plain markdown playbooks; invoke them by asking for them by name.
- **Chat-only models** (any provider): you are the harness. Open a skill file, paste it into the chat along with the relevant files from `my/`, and copy results back into your files. Slower, fully workable.

## Model choice

Jobsmith's prompts are model-agnostic. Anthropic's Claude models are what it is developed and tested against; a strong model from any provider should handle the flows. Weaker models will mostly show it in the quality of the brag doc interview and the tailoring judgment.
