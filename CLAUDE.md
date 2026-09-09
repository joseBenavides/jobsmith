# Jobsmith

Read `AGENT.md` first, every session. It is the full agent definition: who you are, the hard rules, the pipeline model, and the first-run vs. returning behavior.

Skills live in `.claude/skills/`. User data lives in `my/` and only in `my/`.

<!-- BEGIN HOST-PLATFORM (managed by C:\AI\set-platform.ps1 - do not hand-edit) -->
## Host platform - Windows. Do not guess, do not ask.

Jose's workstation runs **Windows 11**. This is settled: never ask "Mac or Windows?",
and never present both options for downloads, installers, browsers, or shortcuts.

- **Commands you hand Jose to run must be PowerShell.** PowerShell 5.1 - not bash, not zsh, not cmd.
- **Paths:** C:\AI\... (backslashes, drive letters). Home is `C:\Users\heyit`.
- **Shortcuts:** Ctrl - describe UI steps as they appear on Windows.
- **Browser:** Chrome on Windows.
- **Never emit** macOS-isms: brew, chmod, sudo, ~/ , /usr/local, `open .`, Cmd-key shortcuts, .dmg / .pkg downloads.
- Use Get-ChildItem / Test-Path / $env:VAR; chain with `;` and `if ($?) { ... }` - PowerShell 5.1 has no `&&`, no ternary, no `??`.
- Your *own* runtime may differ (Claude Code here also exposes Git Bash; cloud
  agents run in Linux containers). That is about your sandbox and says nothing
  about Jose's machine. Anything **he** types by hand is Windows.

Canonical source: `C:\AI\PLATFORM.md`. To change it, run
`powershell -File C:\AI\set-platform.ps1 -Platform <windows|mac|linux>` - once.
<!-- END HOST-PLATFORM -->
