---
name: pickup
description: >-
  Picks up work left by Claude Code or an earlier Antigravity session in this
  repository: reads the git state and the handoff notes, then says what is
  unfinished and what comes next. Use when the user types /pickup, says
  "continue", or opens a project to resume work.
---

# Pick up work

1. Run `git status`, `git branch --show-current`, `git log --oneline -5`,
   `git stash list` and `git fetch origin && git status -sb` (ahead/behind).
2. Read the repository's `AGENTS.md` (its "Handoff for Antigravity" section,
   when there is one) and `PROJECT_CONTEXT.md` (the "Handoff notes" first).
3. Uncommitted changes, a stash, or a feature branch you didn't create are the
   previous agent's unfinished work: read the diff and continue it; never
   reset, discard or overwrite it.
4. If the notes and the code disagree (the previous agent was cut off before
   writing them), trust the code and `git log`, and say so.
5. When the gotchas in `AGENTS.md` call a step in `PROJECT_CONTEXT.md` or
   `README.md` stale (deploy steps especially), follow `AGENTS.md`.
6. Summarise in a few lines: the current branch, what is unfinished, and the
   next step you will take. Production deploys, deletions, secrets and server
   changes still need the owner's yes.
